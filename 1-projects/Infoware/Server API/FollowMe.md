# FollowMe

## FollowMe Navigation Overview

FollowMe is a navigation feature for following pre-defined, complex tours. Rather than calculating routes, FollowMe guides drivers along already specified tracks laid out with exact coordinates. 

Common use cases might include:

 - Waste collection routes
 - Snow plowing or winter road maintenance 
 - Street cleaning operations
 
The FollowMe guided navigation system ensures drivers follow specific tours exactly as they are defined.

## Map Data Compatibility

!!! note "Important" 

	For FollowMe navigation to work correctly, the map data must be consistent across all components: 
	
	- MapTrip mobile application
    - FollowMe Editor
    - MapTrip Server API
    
	This includes matching both map data provider (TomTom, HERE, or OpenStreetMap) and release version (e.g., 2023.03)

### Retrieving Available Map Releases from Server API

If you want too get a list of available map releases, use the following endpoint with a `provider` parameter (TomTom, HERE, or OpenStreetMap):

- `GET /followme/maps`  

The response includes:

- `id`: Unique identifier required for creating FollowMe files
- `provider`: Map data provider name
- `release`: Version of the map data

#### Example Response

``` javascript linenums="1"
[ 
  {
    "id": "TomTom_PLANET_2022_09",
    "provider": "TomTom",
    "release": "2022.09"
  },
  {
    "id": "TomTom_PLANET_2022_12",
    "provider": "TomTom",
    "release": "2022.12"
  },
  {
    "id": "TomTom_PLANET_2023_01",
    "provider": "TomTom",
    "release": "2023.03"
  }
]
```

When creating FollowMe files, use the `id` that matches the map release installed in your MapTrip application.

## Create a FollowMe Folder

FollowMe organizes pre-defined tours (tracks) into folders. Each folder has a unique ID that you'll need when creating FollowMe files. 

!!! note "FollowMe Editor Compatibility"

	The FollowMe Editor currently has limited folder support. If you use both the MapTrip Server API and FollowMe Editor, create files only in the top-level folder. Do not create subfolders through the API. This ensures proper synchronization between both tools. 

If you want to retrieve a list of all of the folders in your account in order to quickly retrieve their `id`, use the endpoint:

- `GET /followme/folder`

To create a new subfolder, use the endpoint with the new folder name: 

- `POST /followme/folder/{folder}` 


After creating a folder, you can proceed to create FollowMe files containing your tour data.

## Creating and Publishing FollowMe Files

### Overview
Getting a tour to your drivers involves three steps:

1. Create a new FollowMe file
2. Add track data to the file
3. Publish the file to MapTrip-enabled navigation devices

### Creating a FollowMe File

Use `POST followme/folder/{folder}/file` to create a file with the following metadata in the body of the request:

- `name`: File name
- `description`: File description
- `map`: Map data release ID
- `creation`: Creation date
- `modification`: Last modification date 


### Adding a Track to the File

The track is a sequence of coordinates that are stored in a CSV file and represent the tour the driver will follow. The track can be created by a GPS logger, by using MapTrip’s recording feature, by the FollowMe editor or by other third party software. 

The requirements for the format of the file are:

- Separator: Semicolon
- First line has to contain column names
- Coordinates: WGS 84 decimal degree (EPSG:4326)
- Valid names for coordinate columns:
	* lat, lon
	* lat, long
	* latitude, longitude
	* xpos, ypos
- Additional columns can be present

Here is an example file:

``` csv linenums="1"
HEADING;SPEED;EVT_TYPE;EVT_DESCR;lon;lat
291.7;0.0;65538;Start collecting;7.140295;50.683959
291.7;0.0;;;7.140295;50.683959
291.7;0.0;;;7.140295;50.683959
291.7;0.7;;;7.140295;50.683965
291.7;0.0;;;7.140295;50.683965
291.7;0.9;;;7.140286;50.683965
291.7;1.9;;;7.140286;50.683965
304.1;10.0;;;7.14025;50.683976
304.9;10.7;;;7.140223;50.683988
310.6;9.6;1;Backwards here;7.140187;50.684005
322.6;8.5;;;7.140169;50.684016
330.9;8.7;;;7.140151;50.684033
0.1;9.8;;;7.140142;50.684056
```

In order to add a track to your recently created file, you will need the folder's `id` and the `name` of your file. To add a track to an existing FollowMe file, use the endpoint `[POST] /followme/folder/{folder}/file/{file}/csv`  with the CSV content included in the body


### Publishing a FollowMe File to a Navigation Device

After creating a FollowMe file on the server using the API, you need to publish it to make the tour available to your drivers' navigation devices. Once published, drivers can follow the predefined tour using their MapTrip application.

Publishing a file requires

- The ID of the folder which contains the file
- The name of the file you want to publish
- A list of device IDs to publish the file to (not needed for `[POST] /followme/folder/{folder}/file/{file}/publish/all`)

In order to query the IDs of your FollowMe devices, use the endpoint `[GET] /followme/devices`. It will return a list of all your devices which are configured for FollowMe. 

To publish the tour to all devices, use the endpoint:

- `[POST] /followme/folder/{folder}/file/{file}/publish/all`

To send the tour to only a certain device or devices, use the endpoint:

- `[POST] /followme/folder/{folder}/file/{file}/publish/devices`


!!! note "Important: Access Control Behavior"

	Publishing a file to a device means that only the specified device has access to the specified file. For example: Publish a file A to two devices 1 and 2. Next publish the same file A only to device 1. The file will then be deleted from device 2.
	
#### Publishing Limitations
You cannot publish a folder or all your files at once (bulk publishing). The folder structure on the server will be recreated on the mobile devices for the files published. 



## Other Useful FollowMe Functions 

### Get track Version History

Tracks often evolve to meet changing needs or for better optimization. For documentation purposes, it may be useful to retrieve previous versions of a FollowMe track as it was driven at an earlier date.

To retrieve previous versions of a track, use the endpoint `[GET] /followme/folder/{folder}/file/{file}/csv/{date}`.

The endpoint requires the following input parameters: 

- ID of the folder 
- Name of the FollowMe file 
- Date of the ride (when the track was driven) 

Tip: You can query the date of the ride by using the endpoint `[GET] /followme/folder/{folder}/file/{file}`. 


### Get Information About Rides

#### What are Rides?

Each time a FollowMe tour is driven, a new ride is automatically created on the server. Remarks and status information can be associated to each ride. 

To query which rides exist for a FollowMe file, you can query the existing rides by using the endpoint `[GET] /followme/folder/{folder}/file/{file}`. 

A ride contains the following attributes: 

- Date of the ride 
- Device ID that drove the ride 
- ID of the ride 
- Remarks: true/false (are remarks available for this ride?) 

#### Get Remarks of a Ride

A remark is a set of notes drivers can save in MapTrip while following a FollowMe tour. It can be used to collect geo-localized feedback from drivers. 

To query the remarks for a specific ride, use the endpoint `[GET] /followme/folder/{folder}/file/{file}/ride/{ride}/remarks`. 

It expects the following parameters: 

- ID of the folder that contains the FollowMe file 
- The name of the FollowMe file 
- ID of the ride 

The response may look like this: 

``` javascript linenums="1" hl_lines="10-11 15-16"
{ 
  "type": "FeatureCollection", 
  "features": [ 
    { 
      "type": "Feature", 
      "id": 1,
      "geometry": { 
        "type": "Point", 
        "coordinates": [ 
          7.143457,
          50.701395
        ] 
      }, 
      "properties": { 
        "UTC_TIME": "1633336992", 
        "TEXT": "Here the trash can is tipped.",
        "CODE": "1" 
      } 
    } 
  ] 
} 
```

The `geometry` of this feature indicates the location where the driver entered this remark. The `properties` contain the time as well as the remark `TEXT`.

#### Get the Status of a Ride

The status of a ride will tell you important information such as sections that were missed or discarded. The ride will have one or more of the following parts: 

- done
- todo
- missed
- discarded

As conveyed by their names, sections might be missed or discarded by a driver. Query the remarks of the ride to see if there are any notes about why. 

To get the status of a ride, use the endpoint `[GET] /followme/folder/{folder}/file/{file}/ride/{ride}/status`. 

It requires the following parameters: 

- ID of the folder that contains the FollowMe file
- Name of the FollowMe file
- ID of the ride

The response may look like this: 

``` javascript linenums="1" hl_lines="21 43 59"
{ 
  "type": "FeatureCollection", 
  "features": [ 
    { 
      "type": "Feature", 
      "id": 1, 
      "geometry": { 
        "type": "LineString", 
        "coordinates": [ // Reduced for example purposes
          [ 
            7.151865, 
            50.695609 
          ], 
          [ 
            7.153572,
            50.69554 
          ] 
        ] 
      }, 
      "properties": { 
        "TYPE": "done", // This section was completed
        "FROM": "0", // The start position (meters)
        "TO": "2812" // The end position (meters)
      } 
    }, 
    { 
      "type": "Feature", 
      "id": 2, 
      "geometry": { 
        "type": "LineString", 
        "coordinates": [ // Reduced for example purposes
          [ 
            7.14193, 
            50.705309 
          ], 
          [ 
            7.141112, 
            50.704974 
          ] 
        ] 
      }, 
      "properties": { 
        "TYPE": "missed", // This section was missed
        "FROM": "2812", // The start position (meters)
        "TO": "5121" // The end position (meters)
      } 
    }, 
    { 
      "type": "Feature", 
      "id": 3, 
      "geometry": { 
        "type": "Point", 
        "coordinates": [ 
          7.153401, 
          50.695546 
        ] 
      }, 
      "properties": { 
        "STATE": "finished", // The tour status
        "POSITION": "2800", // Where on the tour the vehicle is driving (meters) from the beginning of the route
        "LENGTH": "5121" // The total length of the tour (meters)
      } 
    } 
  ] 
}
```
[[Maptrip Detour]]

https://editor.maptrip.de/detour/index.html

In the UI, create a file 
![[Pasted image 20241024110849.png]]

In the Server API:
`[POST] /detour/file`
ID: 85879
Then, get file id 
![[Pasted image 20241024110939.png]]

In the API,  you can get all:
`[GET] /detour/file/all`

You can see all your files here:
![[Pasted image 20241024111055.png]]

In the API:
`[GET] /detour/file/all`
Then using the ID, or all, you can get the segments: 
![[Pasted image 20241024111147.png]]
![[Pasted image 20241024111207.png]]
![[Pasted image 20241024111242.png]]

API:
`/detour/file/{fileid}/segment/all`

To edit the segments in the API, you need to have the `fileid` `segmentid` and `openlr` id: 
File ID: 41333
Segment ID: 1981609
/detour/file/{fileid}/segment/{segmentid}
```json
{
  "id": 1981609,
  "coordinates": [
    {
      "lat": 50.73694734,
      "lon": 7.08814777
    },
    {
      "lat": 50.73848234,
      "lon": 7.08921676
    },
    {
      "lat": 50.73859036,
      "lon": 7.08927964
    },
    {
      "lat": 50.73867563,
      "lon": 7.08933354
    },
    {
      "lat": 50.73947722,
      "lon": 7.09004321
    },
    {
      "lat": 50.74018215,
      "lon": 7.09072593
    },
    {
      "lat": 50.74068242,
      "lon": 7.09122
    }
  ],
  "openlr": "CwUKXCQUYTviCAEzAXY7Ew==",
  "attributes": [
    {
      "name": "MapVersion",
      "value": "201420240408133657"
    },
    {
      "name": "SegmentType",
      "value": "Block"
    },
    {
      "name": "description",
      "value": "test"
    },
    {
      "name": "detourEditor_created",
      "value": "2024-10-24T08:38:15.911Z"
    },
    {
      "name": "detourEditor_modified",
      "value": "2024-10-24T08:42:35.603Z"
    },
    {
      "name": "detourEditor_modifiedBy",
      "value": "keith@infoware.de"
    },
    {
      "name": "detourEditor_originalRoadSpeed",
      "value": "20"
    },
    {
      "name": "direction",
      "value": "3"
    },
    {
      "name": "end",
      "value": "2024-10-24T22:00:00.000Z"
    },
    {
      "name": "mod_restriction",
      "value": "block"
    },
    {
      "name": "start",
      "value": "2024-10-23T22:00:00.000Z"
    },
    {
      "name": "validity",
      "value": "21"
    }
  ]
}
```
7.0942615945122585 50.73334956560983

1. Get a valid coordinate on a road from the editor or another place
2. Use the endpoint [POST] /detour/file/{fileid}/segment/match
		1. This will give you back an array of coordinates & openlr code
		2. Need to update the coordinate array to be a valid list of coordinates 
```json
{
  "coordinates": [
    {
      "lat": 50.73321765,
      "lon": 7.09467852
    },
    {
      "lat": 50.73330294,
      "lon": 7.09444496
    },
    {
      "lat": 50.73342803,
      "lon": 7.09402275
    }
  ],
  "openlr": "CwULjCQTsyObAf++ABUjCg=="
}
```

4. then [POST] /detor/file/{fileid}/segment
	1. paste the result from /match
	2. add a description 
	3. Add the attributes that you want 
		- block
		- delay
		- etc
```json
{
  "id": 1982229,
  "coordinates": [
    {
      "lat": 50.73321765,
      "lon": 7.09467852
    },
    {
      "lat": 50.73330294,
      "lon": 7.09444496
    },
    {
      "lat": 50.73342803,
      "lon": 7.09402275
    }
  ],
  "openlr": "CwULjCQTsyObAf++ABUjCg==",
  "attributes": [
    {
      "name": "Delay",
      "value": "20"
    },
    {
      "name": "MapVersion",
      "value": "201420240408133657"
    },
    {
      "name": "NewSpeed",
      "value": "25"
    },
    {
      "name": "SegmentType",
      "value": "ModifiedSpeed"
    },
    {
      "name": "detourEditor_created",
      "value": "2024-10-24T12:24:56Z"
    },
    {
      "name": "detourEditor_modified",
      "value": "2024-10-24T12:24:56Z"
    },
    {
      "name": "detourEditor_modifiedBy",
      "value": "keith@infoware.de"
    },
    {
      "name": "detourEditor_originalRoadSpeed",
      "value": "30"
    },
    {
      "name": "direction",
      "value": "3"
    },
    {
      "name": "validity",
      "value": "0"
    }
  ]
}
```

##### Response headers

 access-control-allow-credentials

- [ ] edit /detour/file/{fileid}/segment 
post detoue/file/{fileid}/road -> should look if you want to hard code it. 
createdetourroad

createdetoursegement NEEDS TO BE EDITTED 
find in DetourSegmentRequest

- lat: 50.73321765

- lon: 7.09467852

- lat: 50.73330294

- lon: 7.09444496

- lat: 50.73342803

- lon: 7.09402275
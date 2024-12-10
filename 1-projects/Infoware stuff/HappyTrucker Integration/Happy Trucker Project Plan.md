# Goals: 
- Add a button to the MapTripMaps UI. 
- On click, the map will have an overlay with all of the parking places in the area.
- When a user clicks or hovers over a parking icon, they will see a picture and amenities 
- The popup will have a link to book with happy trucker

### Issues: 
- API doesn't provide any link to the booking site. Trying to create a URL from the `name` property doesn't work because there is always a random number at the end of the URL that is not in the response body (not the id). There isn't a way to lead to the website via ID either. I think the only thing we could do with the API as is, is to have a copy function for the name
- https://www.happy-trucker.de/lkw-parkplatz/parkareal-in-bautzen-262?location=Parkplatz-in-bautzen-351

## API: 
#### See parking based on address, route, bounding box, coordinate
```
curl -X 'POST'  'https://test-happy-trucker-backend.it2media.de/v1/parking-areas' -H 'accept: application/json'  -H 'Authorization: Bearer TOKEN' -H 'Content-Type: application/json'  -d '{ "address": "An der Pulvermühle 6, 52349 Düren", "distance": 5000}'

// ParkingAreasRequestBody
{
"boundingBox": {
  "upperLeft": coordinate {lat,lng},
  "lowerRight": coordinate {lat,lng},
  },
"address": string,
"spot": coordinate {lat, lng},
"distance": number (distance in meters for searches around an address, spot, or route),
"numberOfHits": integer,
"features": [list of features ENUM],
"route": [{coordinates, at least 2}],
"availablityCheck": {
  from: IS0-8601 string,
  to: ISO-8601 string
  }
}

// Response
[
  {
    "area": {
      "id": 103,
      "name": "Parkareal Schaustellerbetrieb Raviol in Düren",
      "coordinates": {
        "lat": ,
        "lng"
      },
      ..
      features: [
        {
          "category": "ComfortFeatures",
          "type": "HasRestaurant",
          "description": "has restaurant"
        },
        ..
      ],
      "pictures": [
        {
          "thumbnails": [
            {
              "src": "url",
              "height": 300,
              "width": 400
            }
          ]
        }
      ],
      "spacePrices": [
        {
          "prices": [
            {
              "price": {
                "netPrice": 21.63,
                "grossPrice": 25.7
              },
              "period": "PT24H",
              "isDynamic": false
            },
            {
              "price": {
                "netPrice": 279,
                "grossPrice": 332
              },
              "period": "PT480H", // 20 Days
              "isDynamic": false
            }
          ]
        }
      ]
    }
  }
]
```
# Goals: 
- Add a button to the MapTripMaps UI. 
- On click, the map will have an overlay with all of the parking places in the area.
	- will  have to be from the bounding box as API is currently
- When a user clicks or hovers over a parking icon, they will see a picture and amenities 
- The popup will have a link to book with happy trucker

### Issues: 
- API doesn't provide any link to the booking site. Trying to create a URL from the `name` property doesn't work because there is always a random number at the end of the URL that is not in the response body (not the id). There isn't a way to lead to the website via ID either. I think the only thing we could do with the API as is, is to have a copy function for the name
	- https://www.happy-trucker.de/lkw-parkplatz/parkareal-in-bautzen-262?location=Parkplatz-in-bautzen-351 
	- the `?location=Parkplatz-in-bautzen-351` could be gotten from the `name` attribute, but the `parkareal-in-bautzen-262` cannot
- Cannot match to a route seemingly.  There is a `route` parameter in the request body but it isn't clear how that is used. 
```
[
  {
    "message": "validation error",
    "code": "VALIDATION_ERROR",
    "details": "ParkingAreasRequestBody must only contain one of either bounding box, spot or address. If spot or address is given, distance is mandatory."
  }
]
```

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
"distance": number (distance in meters for searches around an address, spot, or boundingBox),
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

```
curl -X 'POST' \
  'https://test-happy-trucker-backend.it2media.de/v1/parking-areas' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer eyJraWQiOiJhOWQ5NTMzZC1hMGY4LTRmZDItODE1Yy0wZDAwODFjMzQyNjYiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJpbmZvd2FyZSIsImF1ZCI6ImluZm93YXJlIiwibmJmIjoxNzMzODM1MzUyLCJpc3MiOiJodHRwczovL3Rlc3QtaGFwcHktdHJ1Y2tlci1iYWNrb2ZmaWNlLml0Mm1lZGlhLmRlIiwiZXhwIjoxNzMzODM1NjUyLCJpYXQiOjE3MzM4MzUzNTIsImp0aSI6IjRiNWNkMmVkLWQ1YWUtNGNmZi1hOWUyLTIzNzM1YjMxYjJmNSJ9.LTGxUOWiEa164vQYYkxkxY51EwQrn51lMsBsFjAY5IBOfnZWyYxRjSuBGdkVnAjaLV5kv7yA4Blga4EVJXe8xG9Z7JKkLelasRsueAGnzy3zhQcMpKUAfD8dZEXS6LXQ0H1u7kiUFSG4Bjrq12MoioL88eBXtPWWxrS6FmZTsR4cIQI-J7BG6Pl6DTzniMehPIYm3cXg2DnQvTDnp_KJU2taVKLpxrPWs4KpHDUfxEizTW23bAB5CftSw0yT1oN7JPc8JdqjXzYV1wFvHEpL68JFPeJLdSmjwgXiCkRXSBjecb3_nyAuB40UFhNuZYduMgdjaRUN5tdBnQ-NtegMtQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "boundingBox": {
    "upperLeft": {
      "lat": 51.919208,
      "lng": 5.2439296
    },
    "lowerRight": {
      "lat": 50.600158,
      "lng": 10.016115
    }
  },
  "distance": 50000,
  "route": [
    {
      "lat": 52.5163457,
      "lng": 13.3782176
    }
  ]
}'
```
[ticket](https://jira.it2media.de/browse/INWA-4850?jql=project%20%3D%20INWA%20AND%20component%20%3D%20%22MapTrip%20Server%20API%22)

# Steps:
Read tutorial.
See if I can use the `followme` endpoints from the Server Api based on the tutorial.
Ask Georg if that is how you do it. 
Make any improvements to the tutorial based on feedback. 

## First edit:
- Hard to understand
	- "Every map data release has an unique ID. Pick the release you are using in MapTrip from the list and use the ID of the map data release for your FollowMe files." -> Where does a user find this in MapTrip? Do they just know? 
	- Tracks -> what is a track? The route that you've uploaded? 
	- Get the Status of a Ride -> more explanation of the results 

1084897
Roswell_route
2023-11-07~1~aca0817e-ef25-3300-98b3-86b15f403ac2

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "id": 1,
      "geometry": {
        "type": "LineString",
        "coordinates": [
          [
            7.098155,
            50.718956
          ],
          [
            7.098254,
            50.718922
          ],
          [
            7.098676,
            50.718768
          ],
          [
            7.098739,
            50.718745
          ],
          [
            7.098937,
            50.718671
          ],
          [
            7.099305,
            50.718506
          ],
          [
            7.099772,
            50.718285
          ],
          [
            7.100392,
            50.71796
          ],
          [
            7.100787,
            50.717716
          ],
          [
            7.100832,
            50.717693
          ],
          [
            7.101542,
            50.717232
          ],
          [
            7.102135,
            50.716823
          ],
          [
            7.102368,
            50.716652
          ],
          [
            7.102629,
            50.716459
          ],
          [
            7.102934,
            50.716265
          ],
          [
            7.103105,
            50.716146
          ]
        ]
      },
      "properties": {
        "TYPE": "missed",
        "FROM": "0", // ?
        "TO": "539" // ?
      }
    },
    {
      "type": "Feature",
      "id": 2,
      "geometry": {
        "type": "Point",
        "coordinates": [
          7.098748,
          50.71874
        ]
      },
      "properties": {
        "STATE": "finished",
        "POSITION": "115", // ?
        "LENGTH": "539" // ?
      }
    }
  ]
}


```
## The problem
The API already has codes and descriptions for the returned errors:
![[Pasted image 20241125115806.png]]
RFCs 7807 and 9457 define the content type application/problem+json and a JSON format to return error messages with details. The server API is to be converted to this.

Do only additional fields have to be added / can the existing fields be retained?
Should the responses always be adapted or only if Accept: application/json, application/problem+json is set?
Generate corresponding URIs for type from the codes? e.g. DETOUR_ERROR_FILE_DOES_NOT_EXIST-> https://api.maptrip.de/problems/detour/file-does-not-exist
Mapping that resolves these error URIs and returns the description? More details later if necessary?


### Notes:
*Problem Details for HTTP APIs* via [[RFC 7807]] is a standard way for conveying machine-readable error details in an HTTP response. In [[RFC 9457]], new dimensions and updates were added to the framework. 


#### Current response: application/json
```json
{ 
"status": 400, 
"errors": ["An address string has to be provided"], 
"details": [ 
	{ 
	  "code": "GEOCODER_ERROR_MISSING_ADDRESS", 
	  "message": "An address string has to be provided" 
	}
  ] 
}
```
misc.yml -> ApiError & ApiErrorDetail
MaptripServerApiError
#### Updated response: application/problem+json
```json
{
"type": "https://https://api.maptrip.de/docs/tutorial/error-codes.html", // individual error code pages would need to be implemented eventually. General errors that are self-explanatory would lead to about:blank. Absolute URIs are recommended
"title": "Missing Address Parameter",
"status": 400,
"detail": "An address string has to be provided",
"code": "GEOCODER_ERROR_MISSING_ADDRESS",
"instance": "https://stagingapi.maptrip.de/v1/geocoder?provider=TomTom&address=%20&country=DEU&limit=1", // Can get out of request? 
"timestamp": "2023-11-28T12:34:56Z" // Optional but could be useful
}
```

#### Merged to be backward compatible 
```json
{
"status": 400, 
"errors": ["An address string has to be provided"], 
"details": [ 
	{ 
	  "code": "GEOCODER_ERROR_MISSING_ADDRESS", 
	  "message": "An address string has to be provided" 
	}
  ], 
"type": "https://https://api.maptrip.de/docs/tutorial/error-codes.html",
"title": "Missing Address Parameter",
"detail": "An address string has to be provided",
"code": "GEOCODER_ERROR_MISSING_ADDRESS",
"instance": "https://stagingapi.maptrip.de/v1/geocoder?provider=TomTom&address=%20&country=DEU&limit=1",
"timestamp": "2023-11-28T12:34:56Z" 
}
```

ProblemDetail:

type: object

properties:

status:

type: integer

description: HTTP status code

example: 404

type:

type: string

description: A URI leading to more documentation about the problem

example: https://api.maptrip.de/problems/matrix/diameter-too-large

title:

type: string

description: A short message about the error

example: Diameter too large

detail:

type: string

description: Optional additional information about the error

example: The region in which the stops are located must not exceed 200 km in diameter

timestamp:

type: string

description: The time of the error as an ISO-8601 string

example: 2021-07-06T15:02:00.000+0000

instance:

type: string

description: The URI where the error occurred

example: https://api.maptrip.de/v1/matrix/async/77a735b7-f21f-4102-993f-ba1e279ac28a
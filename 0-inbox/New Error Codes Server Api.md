Hi Georg,

I will write this out so that you can read it in your own time. Feel free to just call if you don’t want to read all through this, but it will be beneficial for me to write it out for better understanding on my side.

Currently, this is the response if a client accepts application/json:  
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

If we implemented the application/problem+json from the start, this is how the response should look:  
```json
{
"type": "https://https://api.maptrip.de/docs/tutorial/error-codes.html", // individual error code pages would need to be implemented eventually. General errors that are self-explanatory would lead to about:blank. Absolute URIs are recommended
"title": "Missing Address Parameter",
"status": 400,
"detail": "An address string has to be provided",
"code": "GEOCODER_ERROR_MISSING_ADDRESS",
"instance": "https://stagingapi.maptrip.de/v1/geocoder?provider=TomTom&address=%20&country=DEU&limit=1", // Can get out of request 
"timestamp": "2023-11-28T12:34:56Z" // Optional but could be useful
}
```

```json
{
"type": "https://api.maptrip.de/problems/geocoder/missing-address.html",
"title": "Missing Address Parameter",
"status": 400,
"detail": "An address string has to be provided"
}
```
An option would be to merge the two responses to be backward compatible. If a client accepts either application/json or application/problem+json, the response will be the same. The consideration for this not being the right choice is that it wouldn't be strictly RFC 9457 compliant, it uses redundant information, and it increases the response size. Probably not ideal if we are working on improving our user experience and standardization.
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

Let's say we wanted to provide both options based on what the client sets as the `accept` type. To implement this we would need to:
In `misc.yml`: 
- Create new component `ProblemApiError` which is used instead of the `ApiError` schema on `accept: application/problem+json`
- Modify the `responses`  to reference `ProblemApiError` as well as `ApiError` 
```yml
responses: 
  badRequest: 
    description: ...
    content: 
      application/json:
        schema:
          $ref: '.../ApiError'
      application/problem+json:
        schema:
          $ref: ".../ProblemApiError"
  unauthorized:
  (same)
  tooManyRequests:
  (same)
```

The rest of this might not be accurate as I am not totally familiar with the error handling of the app, but it is a place to start. 

In the app, we would need to add the `ProblemApiError` to the class `ErrorUtils`. We'd need to get the header out of the `RequestService` and serve the response based on that. We'd need to refactor the `ApiExceptionHandler` class to handle the new response shape based on the header. Additionally, we'd need to add the error values to each services error class. In the long range, we'd need to add documentation pages for each of the non-general errors a client might encounter for the `type` value in the response. 
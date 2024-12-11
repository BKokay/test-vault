---
created: 2024-09-27T13:29
updated: 2024-09-27T13:32
---
In the DeviceServiceExceptionTests, I do a better job of checking the `RuntimeException` (line 45) using `assertThrows`
In all of my Service class tests, for the `save()`, I just say it throws an exception. It would be a better test to say what it throws and the message. 

You have to have better return responses from the server for Open API spec. 

Continue with adding Anki cards. Finished in Java - [[Java Generics]] and moving downwards. Have not gotten into database or anything yet. 

Response codes: 
200 - ok
201 - created 
500 - internal server error
400 - bad request 
404 - not found (id)
- [x] are there any other codes I should add? 

For the getAll() methods from the controller, should I add @Hidden? Or do I want them available since it will only be internal 

Changed StreetNumber in db setup to BIGINT from VARCHAR(20)

X Creating DTOs for Update and Save Methods for separation of concerns and security reasons. 

- [x] priceHistory: example in parameter, example return object in API response 200 
- [x] /save is incorrect for request body: says ID of gas station to save, but it should be details. 
- [x] 200 response body in /delete
- [x] Save method to be what is the example street etx
- [x] getDriver response is not correct 
- [x] add **GOOD** comments to my code
- [x] Add better error handling and logging 

## Time Block 10/7
- [x] 9:10 - 12:00 add logs to each methods
	- [x] Check how Georg uses logging in the Server API
- [x] 1 - 3 see what kind of errors could be thrown from each layer (use AI)
	- [x] make sure each error is handled in controller
- [x] Throughout - Add GOOD comments to explain what each layer or method is doing  
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
- [ ] are there any other codes I should add? 

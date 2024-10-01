---
created: 2024-09-27T13:29
updated: 2024-09-27T13:32
---
In the DeviceServiceExceptionTests, I do a better job of checking the `RuntimeException` (line 45) using `assertThrows`
In all of my Service class tests, for the `save()`, I just say it throws an exception. It would be a better test to say what it throws and the message. 

Continue with adding Anki cards. Finished in Java - [[Java Generics]] and moving downwards. Have not gotten into database or anything yet. 
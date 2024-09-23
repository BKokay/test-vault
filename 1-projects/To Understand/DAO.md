---
created: 2024-08-02T13:49
updated: 2024-09-23T11:53
---
Data Access Object. This works as a kind of communicator between the pantry (database) and the chef (program). It consists of five parts:
- A class which defines how your database looks (entity class with annotations)
- An interface for your DAO (just tells the methods)
- An implementation of your DAO (actually has the methods)
- A service worker which talks to your DAO and the main class (calls your dao impl)
- A main class which calls your service worker 
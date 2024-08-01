---
created: 2024-07-26T13:55
updated: 2024-08-01T12:03
---
2024-07-26 14:20
#### DAO (Data Access Object) [[Design Pattern]]
This pattern separates low level data access code from high-level business logic. This [[abstraction]] allows your code to remain modular, easier to test and debug, and easier to maintain. 
**Abstraction Layer** the DAO acts as an intermediary between your application and the database. Instead of writing SQL queries directly into you business logic, you let the DAO interact with the database.
**Operations**
- Create
- Read
- Update
- Delete 
**Encapsulation** The DAO encapsulates the details of the data source (JDBC, JPA, etc.). The client only interacts with the DAO methods, not directly with the database. 

[[java]]
[[Java Links]]
[[Java Design Patterns]]





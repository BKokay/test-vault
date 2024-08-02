---
created: 2024-07-26T13:55
updated: 2024-08-02T11:31
---
2024-07-26 14:20
#### DAO (Data Access Object) [[Design Pattern]] [[Classes needed for design]]
This pattern separates low level data access code from high-level business logic. This [[abstraction]] allows your code to remain modular, easier to test and debug, and easier to maintain. The decoupling of each layer allows you to easily switch out different parts of your program - change the OSM, change the implementation of the database interaction, and create mock implementations for testing. 

**Abstraction Layer** the DAO acts as an intermediary between your application and the database. Instead of writing SQL queries directly into your [[business logic]], you let the DAO interact with the database.
**Operations**
- Create
- Read
- Update
- Delete 

**Encapsulation** The DAO encapsulates the details of the data source (JDBC, JPA, etc.). The client only interacts with the DAO methods, not directly with the database. 

#### in restaurant terms
The **DAO (Data Access Object)** design pattern is like the maître d’ in a restaurant who handles all the interactions with the suppliers and manages the inventory.

In this pattern:

- The **DAO** acts as an intermediary, just like the maître d’. It’s responsible for accessing and managing the restaurant's inventory (the [[database]]), ensuring that the kitchen (your application’s [[business logic]]) gets the ingredients (data) it needs without worrying about where or how the ingredients are stored.
    
- The **business logic** (kitchen) focuses on preparing the dishes (processing data) without having to deal with the complexities of fetching ingredients. The chef doesn't go out to the market—they just ask the maître d’ to bring what they need.
    
- The **database** is like the supplier's warehouse or storeroom, where all the ingredients (data) are stored. The DAO knows how to communicate with this warehouse to get the right ingredients for the kitchen.
    

The advantage of the DAO pattern is that it separates the concerns: the kitchen focuses on cooking (business logic), and the maître d’ handles the inventory and supplier communication (data access). This makes the code easier to maintain and adapt if the way you store or retrieve data changes.

So, the DAO pattern is all about organizing your code so that the business logic (kitchen) doesn’t have to worry about where the data comes from or how it’s stored.

[[java]]
[[Java Links]]
[[Java Design Patterns]]
[[business rules]]
https://www.baeldung.com/java-dao-pattern





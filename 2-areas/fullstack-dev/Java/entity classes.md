---
created: 2024-08-02T09:52
updated: 2024-09-18T14:05
---
An entity class represents a table in a relational database and each instance of an entity class corresponds to a row in that table. 

It is like a recipe card. Just like the recipe card defines the ingredients and instructions for making a dish, and entity class defines the structures of data (fields) and any associated behavior (methods) for and object that represents something in your application.

### Key concepts:
1. Mapping from one class to one database table. The fields of the class represent the columns of the table. 
2. [[entity annotations | Annotations]] that show how to class is mapped to the database schema. The `@Entity` annotation marks a class as an entity and the `@Table` annotation can specify the table name if is it different than the class name. Fields are typically annotated with `@Id` if it is a primary key. `@Column` to specify column details. 
3. Persistence - the [[JDBC]] or other ORM framework  will handle the conversion between Java objects and database records.
4. [[Encapsulation]] of data that is stored in database so you can work with this data as objects in your Java application. 

Key concept in Java applications that interact with databases, particularly when using [[ORM]](Object-Relational Mapping) frameworks like [[JPA Java Persistence API]].

[[java]]
[[programming concepts]]

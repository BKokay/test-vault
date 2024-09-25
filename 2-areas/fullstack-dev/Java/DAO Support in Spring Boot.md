---
created: 2024-09-24T10:44
updated: 2024-09-24T10:47
---

The DAO support in Spring is aimed at making it easy to work with data access technologies (such as JPA, JDBS, or Hibernate) in a consistent way. This lets you switch between the [[persistence technologies]] fairly easily. [[springboot]] [[spring]]

In a normal servlet using [[JDBC]], you'd have the general [[Exceptions]]`SQLException`. In Spring, it is a `DataAccessException`
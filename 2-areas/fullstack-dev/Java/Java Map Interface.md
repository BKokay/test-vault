---
created: 2024-08-13T08:50
updated: 2024-09-03T10:46
---
#### what is a Map? 
It is a data structure that contains values on the basis of key value pairs. Each key value pair is known as an entry. A Map is useful if **you have to update, search, or delete elements on the basis of a key**

#### Implementations of a Map in java
There are two interfaces for implementing a Map in Java: *Map* and *SortedMap*.
There are three classes: *HashMap*, *LinkedHashMap*, and *TreeMap*. 

**Hashmap** is the implementation of Map, but it doesn't maintain any order.
**LinkedHashMap** is the implementation of Map. It inherits HashMap class, but it maintains insertion order.
**TreeMap** is the implementation of Map and SortedMap. It maintains ascending order. 

A Map cannot be traversed, so you need to convert it into Set using *keySet()* or *entrySet()* method. 

[[Map Methods | Other useful Map methods]] [[Java Map.Entry interface]]

[[java]] [[java classes]]
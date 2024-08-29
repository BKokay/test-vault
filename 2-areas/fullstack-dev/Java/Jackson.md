---
created: 2024-08-23T10:13
updated: 2024-08-23T10:26
---
https://www.baeldung.com/jackson-object-mapper-tutorial

```xml
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-core -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-core</artifactId>
    <version>2.17.2</version>
</dependency>

```

//have some example class Car here
use the `writeValue` API to serialize an [[java]] object as [[JSON]] output 
*java class -> JSON*
```java
ObjectMapper objectMapper = new ObjectMapper();
Car car = new Car("purple", "VW Bug");
objectMapper.writeValue(new File("target/car.json"), car);

// {"color":"purple","type":"VW Bug"}

```
The method `writeValueAsString` and `writeValueAsBytes` of `ObjectMapper` class generate a JSON from a Java Object and return the generated JSON as a string or as a byte array. 

use the `readValue` API to deserialize from JSON to java
*JSON -> java class*
```java
//read from string
String json = "{ \"color\" : \"Black\", \"type\" : \"BMW\" }";
Car car = objectMapper.readValue(json, Car.class);

//read from file
Car car = objectMapper.readValue(new File("src/test/resources/json_car.json"), Car.class);

//read from URL
Car car = 
  objectMapper.readValue(new URL("file:src/test/resources/json_car.json"), Car.class);
```
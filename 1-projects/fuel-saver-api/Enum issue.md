---
created: 2024-09-26T13:25
updated: 2024-09-26T13:25
---
I've got a question about enum conversion whenever you have time to respond:

Situation:  Postgres has a fuel_type column for the fuel_stops table. The same values are a Java enum in my API. When trying to update the fuel_type using the java FuelType.Foo, there is a PSQLException thrown b/c 

"column fuel_type is of type fuel_saver.fuel_type but expression is of type character varying." 

Makes sense. So, I found a work around which is just adding `?stringtype=unspecified` to the end of my db url in `application.properties` . It gets my tests to pass, but I don't think it's a good solution. 

Postgres:

```
​CREATE TYPE fuel_type AS ENUM ('DIESEL', 'PETROL', 'ELECTRIC', 'LPG', 'CNG');
```

Add this line: 
```
spring.datasource.url=jdbc:postgresql://localhost:5432/test_db?stringtype=unspecified
```
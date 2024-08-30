---
created: 2024-08-23T10:37
updated: 2024-08-30T18:35
---
### Questions for George
1. JSONObject or new Class()? 
```java
public Optional<List<JSONObject>> getSomething(int id) throws IOException {
}

OR 

public Optional<List<SomeClass>> getSomething(int id){

}
```
Should I be creating classes for each database query that will return more than one row? For example in the DriverDaoImpl getLitersFilled() method, there will be more than one fuel_stop for the driver. So it will be an array of fuel_stop data/objects. These should be classes or can I just use JSONObject? If it is a class, where should I create that class? Could I just make one generic class to fill this in with? 
[[DTO]] - Data Transfer Object - SomeClassDto.java 

2. [[Jackson]] - pretty much only need `objectMapper.writeValue()`? Write to a file? Or write value as a string to return from the API? Probably *string* and return it from my API/servlet layer
	1. return string `writeValueAsString(classObj)`
```java
String carAsString = objectMapper.writeValueAsString(car);
```
3. Insertion order - I like the [[LinkedHashMap]] solution to making sure the order is how I want it. Is that the best way to go about it? 
	- insertion order doesn't matter because later on in implementation it could change
4. save() return boolean? for status codes, I want to have booleans so that I can return 200, 404 statuses
	1. save delete boolean
	2. update return updated object


### Next steps:
[[flow of DAO and DTO]]
- [x] finally finish adding the methods to the DaoImpls
	- [x] Make sure all method have `throws IOException` in the catch block. 
	- [ ] Update fuel_stop.fuel_type to capital letters
	- [x] make sure return statements and types are there
	- [x] Create [[DTO]] classes
	- [x] Remove any methods that will be implemented using the get() method
- [x] add service layer for each Dao
	- [x] pass through status 
- [ ] add servlet layer for each Dao //only for two classes or so
	- [ ] return status codes? 
- [ ] add database into repo with SQL to create the empty database and then another class to populate with test data. 
	- [ ] not class just an sql file with the database creation queries 
- [ ] unit tests - mock data for fake tables then test services
	- [ ] connection test - will be able to see if database works basically
- [ ] connect to SonarQube - java linter, bug finder, tests
	- [ ] code analysis run 
- [ ] SpringBoot 
	- [ ] build controller with one endpoint
	- [ ] add annotations
	- [ ] SpringDoc will create yml
	- [ ] The to SwaggerUI
- [ ] PostGIS (all locations along route)

#### Notes:
* Use UUIDs when creating the 'real' database 
* Specification of API [[open api]] for documentation to use SwaggerUI (code-first vs spec-first)
	* on API layer.
	* Annotations for each method - then Swagger will create that site 
*  SpringDoc will read the annotations and create a spec then the spec will be picked up by Swagger
* Create a spec.yml to have the specs 
* Question to Hendrik: With methods that join tables but still belong to one table, ie. get price history, do I put that in its own servlet or just in the doGet method or make its own method in the GasStationServlet class? 
	* Answer: when it moves to a controller, you will be able to define the endpoints within the GasStationController class. However, for clean code now, maybe it makes sense to make its own servlet. 
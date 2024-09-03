---
created: 2024-07-24T13:36
updated: 2024-09-03T10:24
---
2024-07-24 13:36
Steps write hello world in console in [[java]]
[[apache maven]] convert to this kind of project
add a database driver [[JDBC]] make the connection between JAVA and POSTGRES . WIll need a driver which is a middle wear. Then make with user input
DAO [[DAO Design Pattern]]

Interfaces [[interface-java]]

build a webapp with a [[servlet]] to get one endpoint

[[controller]] [[rest controller]] [[springboot]]

int for regular number, long for bigger numbers , float for floating point, double also floating point but for precision, Boolean 
Every class should go to one file. 
//public everyone can use
private only the class
package globally available in the package. 
[[protected]] - any subclasses can inherit it

### Next steps: 08/15
- [x] add device dao, entity, impl 
- [x] add cascading delete for any foreign keys
- [x] extend with any methods to get complex SQL statements [[Methods for use cases draft]]
	- [ ] check requirements doc
	- [ ] write out method names
	- [ ] write out logic
	- [ ] check with Georg
- [x] add parameterized prepared statement
- [x] add service classes
	- [ ] fuelstop
	- [ ] device
	- [ ] gas station
	- [ ] driver
- [x] Organize code into folders
- [ ] add unit tests using  JMock and JUnit
- [ ] Create a webapp with a servlet

### Project evolves in these steps

- [x] "Hello world" app running in the command line  
- [x] Convert it to an Apache Maven project (for build and dependency management) 
- [x]  Connect to the database via JDBC and print the contents of a table  
-  [x] Read user input from the command line and use it for a driver (e.g. read name of a driver and print all stops of this driver)  
- [x]  Create [[entity classes]] and "Data Access Objects" (DAOs) for each table (see [https://www.digitalocean.com/community/tutorials/dao-design-pattern)](https://www.digitalocean.com/community/tutorials/dao-design-pattern) "https://www.digitalocean.com/community/tutorials/dao-design-pattern)")  
-  [x] Build a webapp with a servlet which reads the name as a HTTP GET parameter and returns a JSON containing the stops  
- [ ] Switch the application to the framework Spring Boot and replace the servlet by a Spring controller  
- [ ] Add all the endpoints to the controller(s)  
- [ ] Add SwaggerUI / for documentation and an interactive UI  
- [ ] Optional: Switch from JDBC to JPA?

### In between these steps

- [x] Use connection pool for DB  
- [x] Logging  [[log4j]]
- [ ] Connect it to Sonarqube  
- [ ] Unit Tests  
- [x] Deregister DB driver on shutdown / restart  
- [ ] Switch from lat / lon to PostGIS  
- [ ] Switch numeric IDs to UUIDs

Great! [[Classes needed for design | About the design]]: You should create one [[entity classes | class]] for every table (Driver, GasStation, FuelStop) and one [[DAO Design Pattern | DAO]] class each. And the main program with the main method in a separate class. And you can start to organize your classes in sub packages, e.g. "domain" for Driver etc., "database" for the database connector and the DAOs - how you organize them is a matter of taste ![🙂]

and it would be nice to have a common interface for the DAO classes, like in this tutorial: [https://www.baeldung.com/java-dao-pattern](https://www.baeldung.com/java-dao-pattern "https://www.baeldung.com/java-dao-pattern")

Should be HTTP return codes
404 - not found
500 - database down , internal server error
log it so we can get the error
on API layer return status code (error/success) 
ALL NEED TO BE PASSED THROUGH LAYERS
I/O exception 500 - add to catch block - e.message() or something 
Empty 404 if(object.isEmpty())
200 Object if(object.)

<**Pattern**>%date %level %class{1.}:%line %msg%n</**Pattern**> add to log.xml

had to add this line to my DB class because [[posgresql]] wasn't connecting
`Class.forName("org.postgresql.Driver").getDeclaredConstructor().newInstance();`

# Open questions:
~~Do I want to return Optional with save, update, or delete? Do I want to return anything from those?~~ 
~~Should I create classes for all of my other methods? No, but what about nested classes? Is that something I should be doing?~~ 

# TODO:
~~The edits I made to GasStationDao need to also be implemented into my other daos.~~ 
~~Add other methods from [[Methods for use cases final]]~~
~~Service Layer [[User Service Class]]~~
~~Servlet [[servlet]]~~
~~Finish getPricePerLiter() in GasStationImpl~~
~~Finish setDriverStatus() in driverimpl~~

!If there is any object that you want to maintain the insertion order, use a [[LinkedHashMap]] [[Java Map Interface]]

08-83-24
"Oh, and one more thing: You can create JSON objects and arrays by creating them by hand with the JSON lib I showed you, but that be a lot of work. For your API, you might want to have a look at [[Jackson]], which is an object mapper. You can use it to serialize Java objects to JSON (or XML) and deserialize JSON (or XML) to Java objects." [[Serialization]]
## Links:




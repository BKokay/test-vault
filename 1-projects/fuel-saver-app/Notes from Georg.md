---
created: 2024-07-24T13:36
updated: 2024-08-22T11:41
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
- [ ] extend with any methods to get complex SQL statements [[Methods for use cases draft]]
	- [ ] check requirements doc
	- [ ] write out method names
	- [ ] write out logic
	- [ ] check with Georg
- [ ] add parameterized prepared statement
- [ ] add service classes
	- [ ] fuelstop
	- [ ] device
	- [ ] gas station
	- [ ] driver
- [ ] Organize code into folders
- [ ] add unit tests using  JMock and JUnit
- [ ] Create a webapp with a servlet

### Project evolves in these steps

- [x] "Hello world" app running in the command line  
- [x] Convert it to an Apache Maven project (for build and dependency management) 
- [x]  Connect to the database via JDBC and print the contents of a table  
-  [x] Read user input from the command line and use it for a driver (e.g. read name of a driver and print all stops of this driver)  
- [x]  Create [[entity classes]] and "Data Access Objects" (DAOs) for each table (see [https://www.digitalocean.com/community/tutorials/dao-design-pattern)](https://www.digitalocean.com/community/tutorials/dao-design-pattern) "https://www.digitalocean.com/community/tutorials/dao-design-pattern)")  
-  [ ] Build a webapp with a servlet which reads the name as a HTTP GET parameter and returns a JSON containing the stops  
- [ ] Switch the application to the framework Spring Boot and replace the servlet by a Spring controller  
- [ ] Add all the endpoints to the controller(s)  
- [ ] Add SwaggerUI / for documentation and an interactive UI  
- [ ] Optional: Switch from JDBC to JPA?

### In between these steps

- Use connection pool for DB  
- Logging  [[log4j]]
- Connect it to Sonarqube  
- Unit Tests  
- Deregister DB driver on shutdown / restart  
- Switch from lat / lon to PostGIS  
- Switch numeric IDs to UUIDs

Great! [[Classes needed for design | About the design]]: You should create one [[entity classes | class]] for every table (Driver, GasStation, FuelStop) and one [[DAO Design Pattern | DAO]] class each. And the main program with the main method in a separate class. And you can start to organize your classes in sub packages, e.g. "domain" for Driver etc., "database" for the database connector and the DAOs - how you organize them is a matter of taste ![🙂]

and it would be nice to have a common interface for the DAO classes, like in this tutorial: [https://www.baeldung.com/java-dao-pattern](https://www.baeldung.com/java-dao-pattern "https://www.baeldung.com/java-dao-pattern")

Should be HTTP return codes
404 - not found
500 - database down , internal server error
log it so we can get the error
on API layer return status code (error/success) 
ALL NEED TO BE PASSED THROUGH LAYERS
I/O exception 500 - add to catch block - e.message() or something 
Empty 404
200 Object 

<**Pattern**>%date %level %class{1.}:%line %msg%n</**Pattern**> add to log.xml

had to add this line to my DB class because [[posgresql]] wasn't connecting
`Class.forName("org.postgresql.Driver").getDeclaredConstructor().newInstance();`

# Open questions:
Do I want to return Optional with save, update, or delete? Do I want to return anything from those? 

# TODO:
The edits I made to GasStationDao need to also be implemented into my other daos. 
Add other methods from [[Methods for use cases final]]
Service Layer [[User Service Class]]
Servlet [[servlet]]
Finish getPricePerLiter() in GasStationImpl
Finish setDriverStatus() in driverimpl

!If there is any object that you want to maintain the insertion order, use a LinkedHashMap [[Java Map Interface]]
## Links:




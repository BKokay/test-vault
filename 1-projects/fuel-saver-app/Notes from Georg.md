---
created: 2024-07-24T13:36
updated: 2024-08-02T10:55
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
### Project evolves in these steps

- [x] "Hello world" app running in the command line  
- [x] Convert it to an Apache Maven project (for build and dependency management) 
- [x]  Connect to the database via JDBC and print the contents of a table  
-  [x] Read user input from the command line and use it for a driver (e.g. read name of a driver and print all stops of this driver)  
- [ ]  Create [[entity classes]] and "Data Access Objects" (DAOs) for each table (see [https://www.digitalocean.com/community/tutorials/dao-design-pattern)](https://www.digitalocean.com/community/tutorials/dao-design-pattern) "https://www.digitalocean.com/community/tutorials/dao-design-pattern)")  
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


## Links:




---
created: 2024-07-24T13:36
updated: 2024-07-25T10:47
---
2024-07-24 13:36
Steps write hello world in console
[[apache maven]] convert to this kind of projecy
add a database driver [[JDBC]] make the connection between JAVA and POSTGRES . WIll need a driver which is a middle wear. THen make with user input
DAO [[dao design pattern]]

Interfaces [[interface-java]]

build a webapp with a [[servlet]] to get one endpoint

[[controller]] [[rest controller]] [[springboot]]

# Project evolves in these steps

- [ ] "Hello world" app running in the command line  
- [ ] Convert it to an Apache Maven project (for build and dependency management) 
- [ ]  Connect to the database via JDBC and print the contents of a table  
-  [ ] Read user input from the command line and use it for a driver (e.g. read name of a driver and print all stops of this driver)  
- [ ]  Create entity classes and "Data Access Objects" (DAOs) for each table (see [https://www.digitalocean.com/community/tutorials/dao-design-pattern)](https://www.digitalocean.com/community/tutorials/dao-design-pattern) "https://www.digitalocean.com/community/tutorials/dao-design-pattern)")  
-  [ ] Build a webapp with a servlet which reads the name as a HTTP GET parameter and returns a JSON containing the stops  
- [ ] Switch the application to the framework Spring Boot and replace the servlet by a Spring controller  
- [ ] Add all the endpoints to the controller(s)  
- [ ] Add SwaggerUI / for documentation and an interactive UI  
- [ ] Optional: Switch from JDBC to JPA?

# In between these steps

- Use connection pool for DB  
- Logging  
- Connect it to Sonarqube  
- Unit Tests  
- Deregister DB driver on shutdown / restart  
- Switch from lat / lon to PostGIS  
- Switch numeric IDs to UUIDs
## Links:




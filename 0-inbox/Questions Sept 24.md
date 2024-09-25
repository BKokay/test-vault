---
created: 2024-09-24T09:51
updated: 2024-09-25T10:44
---
# TODO: 
- [x] tear down database and re put the data using UUID
- [x] Properties for environments 
	- [ ] in folders, but not optimized for anything yet
- [ ] Redo tests for controllers
	- [ ] re-push to sonarqube
- [ ] better exception error hendling

- [ ] SwaggerUI OpenAPI spec 
- [ ] Creating the tables? See question 2
- [ ] Switch to JPA?
- [ ] PostGIS *** for lat/lon
	- [ ] create driver like JDBC 
	- [ ] file to add on to Postgres 
	- [ ] query route and POSTGIS can gind all stations along the line string

## Questions: 
1. In the get(id) methods, I return *Optional.ofNullable()* because it could be an incorrect ID. Should I change this to *Optional.of()* and then handle the null exception? 
	1. not optional.ofNullable() - optional.of() and return empty and handle nullpointexception 
2. Mentioned having the SQL to create the tables. This exists in the test /database package (not yet using jdbcTemplate). However, I wouldn't re-create a table every time, so that isn't something that needs to exist on the fuelsaver level, correct? 
3. application.properties - does it make sense to have test & production here as well for the different profiles? 
	1. https://gitlab.infoware.de/web/maptrip-server-api/-/tree/develop/maptrip-server-api-app/src/main/profiles/production?ref_type=heads

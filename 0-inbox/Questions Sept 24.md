---
created: 2024-09-24T09:51
updated: 2024-09-24T13:31
---
TODO: 
- [ ] Redo tests for controllers
	- [ ] re-push to sonarqube
- [ ] PostGIS *** for lat/lon
- [ ] SwaggerUI 
- [ ] Creating the tables? See question 2
- [ ] Switch to JPA?

## Questions: 
1. In the get(id) methods, I return *Optional.ofNullable()* because it could be an incorrect ID. Should I change this to *Optional.of()* and then handle the null exception? 
2. Mentioned having the SQL to create the tables. This exists in the test /database package (not yet using jdbcTemplate). However, I wouldn't re-create a table every time, so that isn't something that needs to exist on the fuelsaver level, correct? 
3. application.properties - does it make sense to have test & production here as well for the different profiles? 
4. Is there a way to run/build the project without running the tests? 
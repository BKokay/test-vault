---
created: 2024-09-24T09:51
updated: 2024-09-24T11:07
---
TODO: 
- [ ] Redo tests since it is now a controller
- [ ] Creating the table? See question 2
- [ ] SwaggerUI 
- [ ] PostGIS *** for lat/lon
- [ ] Switch to JPA?

## Questions: 
1. In the get(id) methods, I return *Optional.ofNullable()* because it could be an incorrect ID. Should I change this to *Optional.of()* and then handle the null exception? 
2. Mentioned having the SQL to create the tables. This exists in the test /database package (not yet using jdbcTemplate). However, I wouldn't re-create a table every time, so that isn't something that needs to exist on the fuelsaver level, correct? 
3. 
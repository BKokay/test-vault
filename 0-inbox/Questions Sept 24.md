---
created: 2024-09-24T09:51
updated: 2024-09-24T09:54
---
TODO: 
- [ ] Redo tests since it is now a controller
- [ ] SwaggerUI 
- [ ] PostGIS *** for lat/lon
- [ ] Switch to JPA?

## Questions: 
- In the get(id) methods, I return *Optional.ofNullable()* because it could be an incorrect ID. Should I change this to *Optional.of()* and then handle the null exception? 
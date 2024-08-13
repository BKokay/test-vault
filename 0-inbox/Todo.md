---
created: 2024-08-13T13:17
updated: 2024-08-13T13:37
---
- [x] Remove devices_id from fuel_saver.driver 
- [ ] cascading delete - delete method remove everything from driver, then devices, then fuel_stops
- [ ] Method - inactive, active . Inactive drivers will be handled on frontend -  ie show all or show only active etc. 
- [x] company_id rename to have map trip manager:  map_trip_manager_company - bigint remove foreign key

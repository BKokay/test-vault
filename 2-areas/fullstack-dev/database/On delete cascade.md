---
created: 2024-08-15T13:15
<<<<<<< HEAD
updated: 2024-09-04T08:49
=======
updated: 2024-09-23T12:04
>>>>>>> 9bdce39565b602fd1e4387e0e8dddea923455ea8
---
```sql
ALTER TABLE fuel_saver.device
DROP CONSTRAINT device_driver_id_fkey,
ADD CONSTRAINT device_driver_id_fkey FOREIGN KEY (driver_id)
REFERENCES fuel_saver.driver(id)
ON DELETE CASCADE;

ALTER TABLE fuel_saver.fuel_stop 
DROP CONSTRAINT fuel_stop_device_id_fkey, 
ADD CONSTRAINT fuel_stop_device_id_fkey FOREIGN KEY (device_id)
REFERENCES fuel_saver.device(id)
ON DELETE CASCADE

ALTER TABLE fuel_saver.fuel_stop 
DROP CONSTRAINT fuel_stop_station_id_fkey, 
ADD CONSTRAINT fuel_stop_station_id_fkey FOREIGN KEY (station_id)
REFERENCES fuel_saver.gas_station(id)
ON DELETE CASCADE
```

[[sql]] [[database]] #database 
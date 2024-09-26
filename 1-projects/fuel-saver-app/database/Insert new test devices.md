---
created: 2024-09-25T09:30
updated: 2024-09-26T08:35
---
The problem is that the device table has only ids and driver_ids. Both are UUIDs that are automatically generated. I need to use a *subquery* to pull in the driver_id values from the driver table when inserting a new device. 

```sql 
-- Insert new devices, one per existing driver
INSERT INTO fuel_saver.device (driver_id)
SELECT id FROM fuel_saver.driver
ORDER BY id
LIMIT 10; -- Adjust the number here based on how many devices you want to insert

```
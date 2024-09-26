---
created: 2024-09-25T09:53
updated: 2024-09-25T20:58
---
I need to link the fuel stop id with different device ids and station ids. I can enter the queries into pgAdmin like this:
```sql
-- Insert multiple fuel stops for the 2nd device (device with OFFSET 1)
INSERT INTO fuel_saver.fuel_stop (
    device_id, station_id, stop_timestamp, price_per_liter, number_of_liters, total_savings, fuel_type
)
VALUES 
    (
        (SELECT id FROM fuel_saver.device ORDER BY id LIMIT 1 OFFSET 1), -- 2nd device
        (SELECT id FROM fuel_saver.gas_station ORDER BY id LIMIT 1 OFFSET 0), -- 1st station
        '2024-01-01 08:00:00+00', -- Timestamp for fuel stop 1
        1.25,                      -- Price per liter for fuel stop 1
        50.00,                     -- Number of liters for fuel stop 1
        10.00,                     -- Total savings for fuel stop 1
        'DIESEL'::fuel_saver.fuel_type  -- Fuel type for fuel stop 1
    ),
    (
        (SELECT id FROM fuel_saver.device ORDER BY id LIMIT 1 OFFSET 1), -- Same 2nd device
        (SELECT id FROM fuel_saver.gas_station ORDER BY id LIMIT 1 OFFSET 1), -- 2nd station
        '2024-02-05 10:00:00+00', -- Timestamp for fuel stop 2
        1.45,                      -- Price per liter for fuel stop 2
        45.00,                     -- Number of liters for fuel stop 2
        3.00,                      -- Total savings for fuel stop 2
        'PETROL'::fuel_saver.fuel_type  -- Fuel type for fuel stop 2
    ),
    (
        (SELECT id FROM fuel_saver.device ORDER BY id LIMIT 1 OFFSET 1), -- Same 2nd device
        (SELECT id FROM fuel_saver.gas_station ORDER BY id LIMIT 1 OFFSET 2), -- 3rd station
        '2024-03-10 12:00:00+00', -- Timestamp for fuel stop 3
        1.30,                      -- Price per liter for fuel stop 3
        55.00,                     -- Number of liters for fuel stop 3
        5.00,                      -- Total savings for fuel stop 3
        'ELECTRIC'::fuel_saver.fuel_type -- Fuel type for fuel stop 3
    );

```
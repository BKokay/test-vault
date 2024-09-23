---
created: 2024-07-25T08:09
updated: 2024-09-23T12:04
---
2024-07-24 10:34

[[JOIN]] is the basic `INNER JOIN` which takes data from two different tables and congregates it into one joined table. It returns only the rows where there is a match in both tables based on a specified condition. 

##### the syntax: 
```
SELECT columns
	FROM table1
	JOIN table2
	ON table1.common_column = table2.common_column;

```

##### example: 
###### Scenario: Retrieve Drivers and Their Fuel Stops

Let's say you have two tables: `drivers` and `fuel_stops`. You want to retrieve the first name, last name of the drivers, and the timestamp of their fuel stops. You can use the `INNER JOIN` to achieve this.
Tables
**drivers**:

|id|first_name|last_name|devices_id|
|---|---|---|---|
|1|John|Doe|101|
|2|Jane|Smith|102|

**fuel_stops**:

|id|device_id|stop_timestamp|
|---|---|---|
|1|101|2024-07-18 10:00:00+00|
|2|102|2024-07-18 11:00:00+00|
```
SELECT d.first_name, d.last_name, fs.stop_timestamp
FROM fuel_saver.drivers d
JOIN fuel_saver.fuel_stops fs ON d.devices_id = fs.device_id;
```

**Example Output**:

|first_name|last_name|stop_timestamp|
|---|---|---|
|John|Doe|2024-07-18 10:00:00+00|
|Jane|Smith|2024-07-18 11:00:00+00|

#database 

[[practice-problems]] [[ON]] [[sql]]
## Links:




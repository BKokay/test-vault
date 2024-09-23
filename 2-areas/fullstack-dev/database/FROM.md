---
created: 2024-07-25T08:09
updated: 2024-09-23T12:04
---
2024-07-24 09:14
[[FROM]] clause is uses to specify the table or tables you want to retrieve data from. It is fundamental to the [[SELECT]] statement. Can be used to kind of join data from one table, or only query certain columns. 

##### the syntax:

```
SELECT column1, column2
	FROM table_name
```
##### example use case: 

You need to retrieve the names of drivers and details of their fuel stops. 
```
SELECT d.first_name, d.last_name, fs.stop_timestamp, fs.price_per_liter, fs.number_of_liters
	FROM fuel_saver.drivers d
	JOIN fuel_saver.fuel_stops fs ON d.devices_id = fs.device_id
```

[[practice-problems]]

#database  [[sql]]

## Links:




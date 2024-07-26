---
created: 2024-07-25T08:09
updated: 2024-07-25T11:47
---
2024-07-24 09:32

The [[SELECT]] clause specifies the columns to retrieve and can include [[sql expressions]], [[aggregate functions]], and [[aliases]]


##### the syntax:

```
SELECT column1, column2, ... 
	FROM table_name
```
##### example use case: 
You want to retrieve the total number of liters of fuel consumed. [[SUM()]]

```
SELECT SUM(number_of_liters) AS total_liters
	FROM fuel_saver.fuel_stops
```

[[practice-problems]]

#database 

[[sql]]
## Links:




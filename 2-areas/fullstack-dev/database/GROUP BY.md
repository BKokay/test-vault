---
created: 2024-07-25T08:09
updated: 2024-07-25T11:50
---
2024-07-24 08:52
[[GROUP BY]] clause is used to group rows that have the same values in specific columns into aggregate data. It is typically uses in conjunction with [[aggregate functions]] like [[SUM()]]
[[COUNT()]] [[AVG()]] [[MAX())]] and [[MIN()]]. It allows you to perform operations on each group of data rather than on individual rows. 

##### the syntax: 

```
SELECT 
	column_1, 
	column_2,
	...,
	aggregate_function(column_3)
FROM 
	table_name
GROUP BY
	column_1,
	column_2
	...;
```

##### example use case: 

Calculate the total number of liters of fuel consumed by each driver. This will use [[SUM()]]

```
SELECT d.id AS driver_id, SUM(fs.number_of_liters) AS total_fuel_consumed
	FROM fuel_saver.fuel_stops fs
	JOIN fuel_saver.devices dev ON fs.device_id = dev.id
	JOIN fuel_saver.drivers d ON dev.id = d.devices_id
	GROUP BY d.id
	ORDER BY total_fuel_consumed DESC
```

You want to calculate the average salary for each job title. This will use [[AVG()]]

```
SELECT job_title, AVG(salary) AS average_salary
	FROM employees
	GROUP BY job_title
```
[[practice-problems]]


#database 

[[sql]]

## Links:




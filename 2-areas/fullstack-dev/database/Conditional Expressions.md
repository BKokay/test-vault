---
created: 2024-07-25T08:09
updated: 2024-09-03T11:10
---
2024-07-24 10:02

[[Conditional Expressions]] use conditional logic to return different values based on conditions with the `CASE` statement 
[[CASE]]
##### example
```
SELECT id, 
       CASE 
           WHEN number_of_liters > 20 THEN 'Large Stop'
           WHEN number_of_liters BETWEEN 10 AND 20 THEN 'Medium Stop'
           ELSE 'Small Stop'
       END AS stop_size
FROM fuel_saver.fuel_stops;

```

#database 

[[sql expressions]] [[practice-problems]] [[sql]]
## Links:




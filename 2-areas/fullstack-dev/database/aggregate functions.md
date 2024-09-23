---
created: 2024-07-24T22:28
updated: 2024-09-23T11:53
---
2024-07-24 10:32

Perform calculations on a set of values to return a single value using functions like `SUM()`, `COUNT()`, `AVG()`, `MIN()`, and `MAX()`.
##### example
```
SELECT fuel_type, AVG(price_per_liter) AS avg_price_per_liter
FROM fuel_saver.fuel_stops
GROUP BY fuel_type;
```

#database 

[[sql expressions]] [[sql]]

## Links:




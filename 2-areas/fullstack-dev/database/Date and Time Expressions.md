---
created: 2024-07-25T08:09
<<<<<<< HEAD
updated: 2024-09-04T08:49
=======
updated: 2024-09-23T12:04
>>>>>>> 9bdce39565b602fd1e4387e0e8dddea923455ea8
---
2024-07-24 09:51


[[Date and Time Expressions]] perform operations on date and time values using functions like `CURRENT_DATE`, `CURRENT_TIMESTAMP`, `DATE_PART()`, and `AGE()` 

##### example
```
SELECT CURRENT_DATE - INTERVAL '1 day' AS yesterday_date;
```

```
SELECT *
FROM fuel_saver.fuel_stops
WHERE stop_timestamp >= CURRENT_DATE - INTERVAL '7 days';

```

#database 

 [[sql expressions]] [[sql]]
## Links:




---
created: 2024-07-25T08:09
<<<<<<< HEAD
updated: 2024-09-04T08:49
=======
updated: 2024-09-23T12:04
>>>>>>> 9bdce39565b602fd1e4387e0e8dddea923455ea8
---
2024-07-24 10:52
[[WHERE]] clause is used to filter records that meet specific conditions. The criteria must be met in order to the rows to be included in the result set. 

**Purpose**
- filter records
- conditional retrieval 
- combine with other clauses

##### syntax:
```
SELECT column1, column2
FROM table_name
WHERE condition;

```

##### example:
You only want to retrieve drivers who work for a specific company: 
```
SELECT first_name, last_name
	FROM fuel_saver.drivers
	WHERE company_id = 1;
```

#database 
[[sql]]
## Links:




2024-07-24 11:03
What is the difference between [[WHERE]] and [[CASE]] in [[Conditional Expressions]]?

- **Purpose**:
    - **WHERE**: Filters rows in a query based on specified conditions.
    - **CASE**: Returns different values based on conditions within a query, often used to create new computed columns.
- **Context**:
    - **WHERE**: Used in `SELECT`, `UPDATE`, `DELETE`, and other data manipulation statements to filter rows.
    - **CASE**: Used within `SELECT` statements, and occasionally in `ORDER BY` or `GROUP BY` clauses to create conditional expressions.
- **Result**:
    - **WHERE**: Filters the entire row based on the condition.
    - **CASE**: Evaluates conditions for individual columns or expressions and returns corresponding results.

##### example of WHERE and CASE used together
**Scenario:** Retrieve drivers who have made fuel stops and classify their fuel stops based on the number of liters. 

```
SELECT d.first_name, d.last_name, fs.number_of_liters,
		CASE 
			WHEN fs.number_of_liters > 20 THEN 'Large Stop'
			WHEN fs.number_of_liters BETWEEN 10 AND 20 THEN 'Medium Stop'
			ELSE 'Small Stop'
		END AS stop_size
	FROM fuel_saver.drivers d
	JOIN fuel_saver.fuel_stops fs ON d.devices_id = fs.device_id
	WHERE fs.number_of_liters > 5; 
```

#database [[sql]] [[practice-problems]]
## Links:




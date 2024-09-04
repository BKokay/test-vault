---
created: 2024-07-25T08:09
updated: 2024-09-04T08:49
---
2024-07-24 10:11
	First evaluates the expression and compares the result with each value( `value1, value2, ...`) in the `WHEN` clauses sequentially until it finds the match. 
	
Once the result of the `expression` equals a value (value1, value2, etc.) in a `WHEN` clause, the `CASE` returns the corresponding result in the `THEN` clause.

If `CASE` does not find any matches, it returns the `else_result` in that follows the `ELSE`, or `NULL` value if the `ELSE` is not available.

##### example
Use a `CASE` expression to add the rating description to the output:
```
SELECT title,
       rating,
       CASE rating
           WHEN 'G' THEN 'General Audiences'
           WHEN 'PG' THEN 'Parental Guidance Suggested'
           WHEN 'PG-13' THEN 'Parents Strongly Cautioned'
           WHEN 'R' THEN 'Restricted'
           WHEN 'NC-17' THEN 'Adults Only'
       END rating_description
FROM film
ORDER BY title;
```

Output:

| title            | rating | rating_description               |
|:-----------------|:-------|:---------------------------------|
| Academy Dinosaur | PG     | Parental Guidance Suggested      |
| Ace Goldfinger   | G      | General Audiences                |
| Adaptation Holes | NC-17  | Adults Only                      |
| Affair Prejudice | G      | General Audiences                |
| African Egg      | G      | General Audiences                |
| Agent Truman     | PG     | Parental Guidance Suggested      |
| Airplane Sierra  | PG-13  | Parents Strongly Cautioned       |



#database
 [[sql expressions]] [[practice-problems]]
## Links:




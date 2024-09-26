---
created: 2024-07-25T08:09
updated: 2024-09-26T08:35
---
2024-07-24 10:11
Evaluates as a normal `if/else`. When the first condition that returns true happens, the function returns the corresponding result that follows that condition. It stops evaluating after finding a `true` condition. 

##### example: 
Say we have this table and we want to do the following:
- If the length is less than 50 minutes, the film is short.
- If the length is greater than 50 minutes and less than or equal to 120 minutes, the film is medium.
- If the length is greater than 120 minutes, the film is long.

| film         |
| ------------ |
| *film_id     |
| title        |
| description  |
| release_year |
| length       |
| duration     |
| ...          |
We can use the `CASE` expression in the [[SELECT]] statement: 
```
SELECT 
  title, 
  length, 
  CASE WHEN length > 0 
  AND length <= 50 THEN 'Short' WHEN length > 50 
  AND length <= 120 THEN 'Medium' WHEN length > 120 THEN 'Long' END duration 
FROM 
  film 
ORDER BY 
  title;
```

Output: 

| title              | length | duration |
|:-------------------|-------:|---------:|
| Academy Dinosaur   |     86 |   Medium |
| Ace Goldfinger     |     48 |    Short |
| Adaptation Holes   |     50 |    Short |
| Affair Prejudice   |    117 |   Medium |
| African Egg        |    130 |     Long |
| Agent Truman       |    169 |     Long |


[[#database]]

[[sql expressions]] [[practice-problems]] [[sql]]
## Links:




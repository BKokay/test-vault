## [Fundamentals] Even

For this assessment, you should submit 2 functions:

**Function 1**: `even`
The first function, `even` should take an integer (`n`) as input and return a boolean value indicating whether or not `n` is even.

`even(12)` should return `true`.

1. [[Precisely define the problem]] 
	- even(n) -> if n is even, return true
2. [[Develop reasonable strategies]]
	- if check n%2 === 0 return true, else return false
	- if (n/2 === 0) -> true
3. [[Choose a strategy based on your criteria]]
	- use `%` as it is best practice
4. [[Create a top-down outline of your strategy]]
	- define function
	- check `n%2` 
	- if `=== 0` -> true, else false
5. [[Implementation]]
```javascript
/* Summary: Check if the remainder of `n` divided by 2 is equal to 0 using the modulus operator */

function even(n) {
    // If the remainder is 0, return true
    if (n%2 === 0) {
        return true;
    // Otherwise, return false
    } else {
        return false; 
    }
}

```

**Function 2**: `allEven`
The second function, `allEven` should take an array of integers as input and return a boolean value indicating whether or not _all_ of the integers in that array are even.

`allEven([2, 4, 2, 9])` should return `false`.

1. [[Precisely define the problem]]
	- allEven(array) -> if every number in the array is even, return true
	-  allEven([n1, n2, n3, ...]) -> if n[i] are all even, return true
2. [[Develop reasonable strategies]]
	- 


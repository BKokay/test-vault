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
/* Summary: Determine if a number is even by checking if the remainder of the number divided by 2 is 0. */

function even(n) {
    // If the remainder of n%2 is 0, the number is even. Return true.
    if (n%2 === 0) {
        return true;
    // Otherwise, the number is odd. Return false.
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
	- iterate through the array using n[i] % 2. If it is not 0, return false. 
	- Could I do this with while()?
		- while n[i]%2 === 0 then what? 
3. [[Choose a strategy based on your criteria]]
	- iterate using a for-loop
4. [[Create a top-down outline of your strategy]]
	- define function
	- loop through array
	- create if statement looking for false
5. [[Implementation]]
```javascript
/* Summary: Check if all numbers in the array are even by making sure no number has a remainder when divided by 2. */

function allEven(nums) {
    // Iterate over all the numbers in the array
    for (let i = 0; i < nums.length; i++) {
        // If the remainder of the current number divided by 2 is not 0, the number is odd.
        if (nums[i]%2 !== 0) {
            // An odd number was found. Return false. 
            return false
        }
    }
    // No odd numbers were found. Return true. 
    return true; 
}
```


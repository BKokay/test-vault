Should be three functions. The first checks in the number is > 10. The second takes an array of two numbers and return the largest of the two. The third takes three numbers and returns the largest of the three. 

```javascript
/* Summary: Check if a number is bigger than 10 and return a boolean. */
function large(number) {
    // Do check
    if (number > 10) {
	    return true;
    } else {
        return false; 
    }    
}

/* Summary: Compare two numbers. Return the largest. */
function larger(numOne, numTwo) {
    // Compare the numbers. Return the largest.
    if (numOne >= numTwo) {
        return numOne;
    } else { 
        return numTwo; 
    }
}

/* Summary: Compare three numbers. Return the largest. */
function largest(numOne, numTwo, numThree) {
    let largest; 
    
    // Compare numbers
    if (numOne >= numTwo && numOne >= numThree) {
        largest = numOne;
    } else if (numTwo >= numOne && numTwo >= numThree) {
        largest = numTwo;
    } else if (numThree >= numOne && numThree >= numTwo) {
        largest = numThree; 
    }
    // Return the largest
    return largest; 
}

```

The first function, `large`, should take a number as input and return a boolean value indicating whether or not that number is larger than 10.

`large(9)` should return `false`.

The second function, `larger`, should take two numbers as input, and it should return the largest argument.

`larger(3, 10)` should return 10.  
`larger(12, 12)` should return 12.

The third function, `largest`, should take three numbers as input, and it should return the largest argument.

`largest(12, 14, 10)` should return 14.
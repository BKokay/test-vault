Should be three functions. The first checks in the number is > 10. The second takes an array of two numbers and return the largest of the two. The third takes three numbers and returns the largest of the three. 

```javascript
// Summary: A function that checks if an argument is greater than 10. The argument is a number and the return type is a boolean. 

function large(number) {
    // If the number is greater than 10, it is considered 'large', and we return true
    if (number > 10) {
	    return true;
    } else {
        return false; 
    }    
}

// Summary: Check which of the two numbers provided as arguments to the function is larger. Return the larger of the two. 
function larger(numOne, numTwo) {
    // If numOne is greater or equal to numTwo, it is the largest, so we return numOne
    if(numOne >= numTwo) {
        return numOne;
    } else {
    // If we didn't return numOne, that is because numTwo is the largest. 
        return numTwo; 
    }
}

// Summary: Check which of three number arguments is the largest and return that number
function largest(numOne, numTwo, numThree) {
    var largest; 
    
    // Is numOne bigger than the other two? If so, to assign largest 
    if(numOne >= numTwo && numOne >= numThree) {
        largest = numOne;
    }
    // Is numTwo bigger than the other two? If so, assign to largest
    if(numTwo >= numOne && numTwo >= numThree) {
        largest = numTwo;
    }
    // Is numThree bigger than the other two? If so, assign to largest
    if(numThree >= numOne && numThree >= numTwo) {
        largest = numThree; 
    }

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
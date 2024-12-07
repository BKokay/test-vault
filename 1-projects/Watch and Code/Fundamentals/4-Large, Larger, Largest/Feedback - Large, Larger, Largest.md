### Learnings:
- I get caught up in variable names still. Because I wanted to explicitly show that the number was largest, I set up an empty variable called `largest` to store the value. This step was not needed, because I could have just returned the argument value after each statement checking which was bigger. 
- Type of error: #pedantic #overexplanation 
- #Feedback 
```javascript 
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

// Feedback on this problem: -10 points for design because setting the greatest num to largest in each if-block suggests that we *have to* keep looking for largest. The better option would be that you just return the number in the body of each if-block. 

// Suggested solution:
// Summary: For each number, check if it's larger than (or equal to) the others. 

function largest(a, b, c) {
  // Is a the largest?
  if (a >= b && a >= c) {
    return a;
  }

  // Is b the largest?
  if (b >= a && b >= c) {
    return b;
  }

  // Is c the largest?
  if (c >= a && c >= b) {
    return c;
  }
}

```

### Other notes: 
- The summary should be in the format `/* ... */`
- Make sure to have spaces after if/ else-if
- only use `let` to declare variables
- Don't be overly wordy with comments - short and to the point. Gordon/Lily even use questions 
- 
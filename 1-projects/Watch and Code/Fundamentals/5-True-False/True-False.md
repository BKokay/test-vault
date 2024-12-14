## [Fundamentals] True / False

For this assessment, you should submit 3 functions.

**Function 1: `canWatchTv`**

Imagine that you only allow yourself to watch tv on weekends or holidays. Write a function that takes two boolean values as input: `isHoliday` and `isWeekday`. As their names suggest, `isHoliday` tells you if the day in question is a holiday, and `isWeekday` tells you if the day in question is a weekday (i.e. not a weekend). Return a boolean value indicating whether or not you can watch tv.
1. [[Precisely define the problem| Define the Problem: ]]
	- function canWatchTv(boolean isHoliday, boolean isWeekday) -> isHoliday? return true
2. [[Develop reasonable strategies| Develop a strategy]]
	- have a single if-block and return false if weekend. Otherwise return true. 
	- Since variables are booleans, could just return the weekday. Would that be confusing?
3. [[Choose a strategy based on your criteria| Make a choice]]
	- I think trying the second strategy is the best option but with a note that I want to see the feedback on the choice so I can better learn which way is best. 
4. [[Create a top-down outline of your strategy| Make an outline]]
	- define the function
	- check if it is a weekday -> return weekday
	- return holiday
5. [[Implementation]]
```javascript
/* Question: since isHoliday and isWeekday both hold the boolean value I would want to return, would it be more readable to return those values explicityly rather than true/false? I decided against this since the function name asks a question and true/false seemed more readable to me, but I would like your opinion. */
// ANSWER: true false is more clear

//Submission 1 - missing check for if it is a weekend
/* Summary: Return true if you can watch TV and false if not. */

function canWatchTv(isHoliday, isWeekday) {
    // Check if it's a weekday.
    if (isWeekday) {
        // You can't watch TV
        return false;
    } 
    // Not a weekday? You can watch TV
    return true;
}

// Submission 2 - The first challenge is to make sure that you express it _correctly_. The second challenge is to think about how you can express it _clearly_.

function canWatchTv(isHoliday, isWeekday) {
  // If it's a holiday, return true.
  if (isHoliday === true) {
    return true;
  }

  // If it's NOT a weekday, return true.
  if (isWeekday === false) {
    return true;
  }

  // Otherwise, return false.
  return false;
}
```

**Function 2: `doTheyAgree`**

Two business partners are trying to make a decision, and they want to know if they agree with each other. Write a function that takes two boolean values as input (`partner1Decision` and `partner2Decision`), and return a boolean value indicating whether or not their decisions are the same.
1. [[Precisely define the problem | Definte the problem]]
-  the two inputs are booleans
- We want to know if they are equal
2. [[Develop reasonable strategies | Develop a stragegy]]
- one if check to see if they are equal
- if they are equal, true
- either return false after the if check or use an else clause
3. [[Choose a strategy based on your criteria| Choose]]
- I think the else clause would be more readable
4. [[Create a top-down outline of your strategy | Make and outline]]
- Define function
- Check for equality
- Return boolean
5. [[Implementation]]
```javascript
/* Summary: return true if both partners have the same value. */

function doTheyAgree(partner1Decision, partner2Decision) {
    // Do they agree?
    if (partner1Decision === partner2Decision) {
        return true;
    } else {
        // They don't agree.
        return false; 
    }
}
```

**Function 3: `isOpen`**

Imagine a store that’s open every day of the week, except for Mondays. The store is also _closed_ for the entire month of July. Write a function that takes two strings as input: `weekday` and `month`. Your function should return a boolean value indicating whether or not the store is open on the indicated day.

You can assume that the `weekday` will be one of these strings: `"monday"`, `"tuesday"`, `"wednesday"`, `"thursday"`, `"friday"`, `"saturday"`, `"sunday"`.  
You can also assume that `month` will be one of these strings: `"january"`, `"february"`, `"march"`, `"april"`, `"may"`, `"june"`, `"july"`, `"august"`, `"september"`, `"october"`, `"november"`, `"december"`.

- [[Precisely define the problem| Define the problem]]
- A function that returns false if the weekday is `"monday"` or if the month is `"july"` 
- [[Develop reasonable strategies| Develop strategies]]
- Check if day = monday OR month = july return false; 
- Have if/ if-else statements
- Have two if statements
- [[Choose a strategy based on your criteria | Choose a strategy]]
- The most readable is maybe the combined || 
- [[Create a top-down outline of your strategy]]
- define function
- check if Monday || July-> false
- Return true
- [[Implementation]]
```javascript
/* Summary: check for closed days and return true; otherwise, return false. */

function isOpen(weekday, month) {
    // Check for known closed periods.
    if (weekday === "monday" || month === "july") {
        // Store is closed.
        return false;
    } 
    // Store is open.
    return true; 
}
```
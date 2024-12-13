When you run JavaScript in a file or in the console, Chrome will take your code and insert it into an anonymous function. It will then immediately run that function. Here's how:

First, Chrome will create an anonymous function. Since anonymous function declarations are illegal, Chrome will surround the function with parentheses as a workaround.
```javascript
(function() { 
});
```

Your code is then inserted into the body of the anonymous function like so:
```javascript
(function() { 
    // Your code
});
```

Now, Chrome wants to run your code. As you know, if you want to run a function, you just add a set of parentheses to the end.
```javascript
(function() { 
    // Your code
})(); // Calling the function
```

How it will look:
```javascript
(function() { 
    console.log('hi');
});
```

Since we are running a function, it'll get added to the call stack, but since the function is unnamed, it will show up as (anonymous) in the call stack.
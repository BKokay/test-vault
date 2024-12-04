## Operators:

```
// Mathematical operators
+, -, *, /, %, **, +=, -= 

--, ++ (ONLY when used as variableName++ or variableName--)

// Logical operators
===, !==, >, >=, <, <=, !, ||, &&
```

## Declaring variables:

```
let variableName = expression;
```

## Simple assignment:

```
// Assign a value to a variable.
variableName = expression;

// Assign a value to a property.
myObject.myProperty = expression;
```

## Declaring functions:

```
function functionName(argument1, argument2, ...) {
  // body
  return value; // optional
}
```

## Iteration:

```
for (let i = 0; i < x; i++) {
  // body
}

while (condition) {
  // body
}
```

## Conditional structures (if/else if/else):

```
// if-statement
if (condition) {
  // block
}

// if/else-statement
if (condition) {
  // block 1
} else {
  // block 2
}

// if/else-if/else statement
if (condition) {
  // block 1
} else if (condition) {
  // block 2
} else {
  // block 3
}
```

## Arrays:

```
// Creating an array.
let myArray = [element1, element2, ...];

// Reading from an array.
myArray[index] // returns element

// Writing to an array.
myArray[index] = expression;

// Accessing length.
myArray.length

// Updating length. For example, removing last item:
myArray.length = myArray.length - 1;

// No built-in array methods are allowed. To write to an
// array, you must use the technique above.
```

## Objects:

```
// Creating an object.
let myObject = {
  property1: expression,
  property2: expression,
};

// Reading from an object.
myObject.property1
myObject[expression]

// Writing to an object.
myObject.property1 = expression;
myObject[expression] = expression;

// Iterating over properties.
for (let property in myObject) {
  console.log(property);
}

// No built-in object methods are allowed.
```

## Strings:

```
// Accessing a single character in a string.
myString[index]

// Accessing string length.
myString.length

// No built-in string methods are allowed.
```

## Allowed Primitive Data Types:

```
numbers, booleans, strings, undefined, and null
```
---
created: 2024-08-20T11:45
updated: 2024-08-21T21:47
---
# metaphor to help understand
Using `java.util.Optional` is like having a special covered dish in a restaurant that might or might not contain food. You don't want to be surprised when the waiter takes the cover off and you get an empty plate. Similarly, you don't want your program to crash when a method unexpectedly returns `null` . `Optional` helps you to deal with these situations by forcing you to deal with the possibility that the value might be absent. 

## Key operations with `Optional`
1. Creating an optional
	1. Full Dish (`Optional.of`): If you know there is food (data), you use `Optional.of(value)`
	2. If there is nothing there, use `Optional.empty()`
	3. If you are not sure if there is data, user `Optional.ofNullable(value)`
2. Checking the value (`isPresent`):
	1. You can check if there is a value using `isPresent()`
```java
Optional<String> fullDish = Optional.of("Pasta");
Optional<String> possiblyEmptyDish = Optional.ofNullable(maybeFood);
if(fullDish.isPresent()){
	doSomethingHere(); 
}
```
---
created: 2024-07-31T10:41
updated: 2024-07-31T11:24
---
Lambda expressions allow you to write more concise and readable code when dealing with [[functional interfaces]]. They provide a way to create anonymous methods that can be passed around as if they were objects. They are comparable to [[javascript arrow functions]]. 

### Syntax:
- (parameters) -> expression
- (parameters) -> {statements}
```java
(int a, int b) -> a + b //will return their sum 
```

[[lambda expressions compare/contrast examples]]

### Benefits: 
1. Conciseness
2. Improved readability 

### Use cases: 
1. Collection manipulation (`forEach`, `map`, `filter`, etc)
2. event handling 
3. threading (`Runnable`) [[what is a thread]]
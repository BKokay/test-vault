---
created: 2024-07-31T10:56
updated: 2024-07-31T12:03
---
[[java]] 
## Example 1: Basic

```java
// Without:
Runnable runnable = new Runnable() {
	@Override
	public void run(){
		System.out.println("Running...");
	}
};

//With: 
Runnable runnable = () -> System.out.println("Running...");
```
[[What is a runnable]]
## Example 2: Using a Lambda with a `Comparator`
Sorting a list of strings by length:
```java
//without:
Comparator<String> comparator = new Comparator<String>() {
	@Override
	public int compare(String s1, String s2){
		return Integer.compare(s1.length(), s2.length());
	}
};

//with:
Comparator<String> comparator = (s1, s2) -> Integer.compare(s1.lenth(), s2.length());
```
[[what does @Override do]]
[[what is a Comparator]]
## Example 3: Passing Lambdas to Methods
You can pass [[lambda expressions]] directly to methods that expect a functional interface. Here, we will pass an array to the forEach method. [[java arrays]] [[java methods]]
```java
List<String> list = Arrays.asList("apples", "bananas", "peaches");

//without: 
list.forEach(new Consumer<String>() {
	@Override
	public void accept(String s){
		System.out.println(s); 
	}
});

//with:
list.forEach(s -> System.out.println(s));

//with method reference (even simpler)
list.forEach(System.out::println);
```
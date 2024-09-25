---
created: 2024-09-18T13:28
updated: 2024-09-25T20:58
---
### Important intermediate operations: 
[[how to read java syntax with generics]]
1. .map() 
[[map()]]
```java
<R> Stream<R> map(Function<? super T, ? extends R> mapper)
```
2. .filter()
[[filter()]]
```java
Stream<T> filter(Predicate<? super T> predicate)
```
3. .sorted()
[[sorted()]]
```java
Stream<T> sorted()  
Stream<T> sorted(Comparator<? super T> comparator)
```
4. .flatMap()
[[flatMap()]]
```java
<R> Stream<R> flatMap(Function<? super T, ? extends Stream<? extends R>> mapper)
```
5. .distinct()
[[distinct()]]
```java
Stream<T> distinct()
```
6. .peek()
[[peek()]]
```java
Stream<T> peek(Consumer<? super T> action)
```

Java program which demonstrates the use of all intermediate operations:
```java
import java.util.Arrays;
import java.util.HashSet;
import java.util.List;
import java.util.Set;
import java.util.stream.Collectors;

public class StreamIntermediateOperationsExample {
    public static void main(String[] args) {
        // List of lists of names
        List<List<String>> listOfLists = Arrays.asList(
            Arrays.asList("Reflection", "Collection", "Stream"),
            Arrays.asList("Structure", "State", "Flow"),
            Arrays.asList("Sorting", "Mapping", "Reduction", "Stream")
        );

        // Create a set to hold intermediate results
        Set<String> intermediateResults = new HashSet<>();

        // Stream pipeline demonstrating various intermediate operations
        List<String> result = listOfLists.stream()
            .flatMap(List::stream)               // Flatten the list of lists into a single stream
            .filter(s -> s.startsWith("S"))      // Filter elements starting with "S"
            .map(String::toUpperCase)            // Transform each element to uppercase
            .distinct()                          // Remove duplicate elements
            .sorted()                            // Sort elements
            .peek(s -> intermediateResults.add(s)) // Perform an action (add to set) on each element
            .collect(Collectors.toList());       // Collect the final result into a list

        // Print the intermediate results
        System.out.println("Intermediate Results:");
        intermediateResults.forEach(System.out::println);

        // Print the final result
        System.out.println("Final Result:");
        result.forEach(System.out::println);
    }
}

//Results:
Intermediate Results:
STRUCTURE
STREAM
STATE
SORTING
Final Result:
SORTING
STATE
STREAM
STRUCTURE

```

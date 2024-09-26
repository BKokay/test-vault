---
created: 2024-09-23T13:08
updated: 2024-09-25T20:58
---
# Definition
A feature that will allow your code to work with different types while providing type safety at compile-time. 

## Why use them?
1. *Type Safety*: code will still be checked for types when compiled
2.  *Code Reusability*: write a class or a method that can work with different types
3. *Type Erasure*: They are removed at runtime so you have backwards compatibility
4. *Wildcards*: If you don't know what you are going to get
5. *Bounded Type Parameters*: Restrict the types that can be used with a generic class or method. [[bounded generics]]

### Best Practices
1. Use meaningful names for type parameters: 
	- T for type
	- E for element
	- K for key
	- V for value
2. Prefer using generics over raw types for type safety.

```java
public class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() { return key; }
    public V getValue() { return value; }

    public static <T extends Comparable<T>> T max(T a, T b) {
        return a.compareTo(b) > 0 ? a : b;
    }
}

// Usage
Pair<String, Integer> pair = new Pair<>("Age", 30);
Integer maxValue = Pair.max(5, 10);
```

[[java]] 
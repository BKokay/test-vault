---
created: 2024-08-12T10:10
updated: 2024-09-02T08:50
---
NullPointerException - this can happen with a program has an abnormal termination. 
Example is with this code:
```java
public class OptionalDemo {
    public static void main(String[] args)
    {
        String[] words = new String[10];
        String word = words[5].toLowerCase();
        System.out.print(word);
    }
}
```
The system will throw this error:
```
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "String.toLowerCase()" because "words[5]" is null

at de.infoware.test.OptionalDemo.main(OptionalDemo.java:6)
```

To avoid this mistake, we can use an java.util.Optional class so our program can execute without crashing. 
Here is the implementation:
```java
// Java program with Optional Class

import java.util.Optional;

// Driver Class
public class OptionalDemo {
      // Main Method
    public static void main(String[] args)
    {
        String[] words = new String[10];
        
          Optional<String> checkNull = Optional.ofNullable(words[5]);
        
          if (checkNull.isPresent()) {
            String word = words[5].toLowerCase();
            System.out.print(word);
        }
        else
            System.out.println("word is null");
    }
}
```

Further examples:
```java 
// Java program to illustrate
// optional class methods

import java.util.Optional;

class GFG {

    // Driver code
    public static void main(String[] args)
    {

        // creating a string array
        String[] str = new String[5];

        // Setting value for 2nd index
        str[2] = "Geeks Classes are coming soon";

        // It returns a non-empty Optional
        Optional<String> value = Optional.of(str[2]);

        // It returns value of an Optional.
        // If value is not present, it throws
        // an NoSuchElementException
        System.out.println(value.get());

        // It returns hashCode of the value
        System.out.println(value.hashCode());

        // It returns true if value is present,
        // otherwise false
        System.out.println(value.isPresent());
    }
}

---
// Java program to illustrate
// optional class methods

import java.util.Optional;

class GFG {

    // Driver code
    public static void main(String[] args)
    {

        // creating a string array
        String[] str = new String[5];

        // Setting value for 2nd index
        str[2] = "Geeks Classes are coming soon";

        // It returns an empty instance of Optional class
        Optional<String> empty = Optional.empty();
        System.out.println(empty);

        // It returns a non-empty Optional
        Optional<String> value = Optional.of(str[2]);
        System.out.println(value);
    }
}

```
To find more information, check this article: https://www.geeksforgeeks.org/java-8-optional-class/ 
[[java]] [[java.util]] [[java optional metaphor]]
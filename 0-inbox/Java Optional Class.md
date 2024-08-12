---
created: 2024-08-12T10:10
updated: 2024-08-12T10:20
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


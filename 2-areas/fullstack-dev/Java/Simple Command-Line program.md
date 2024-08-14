---
created: 2024-07-30T13:23
updated: 2024-08-14T11:25
---
[[java.util]] [[java.util.Scanner]] [[java]]

```java

import java.util.Scanner;

public class CommandLineInteraction {
    public static void main(String[] args) {
        // Create a Scanner object to read input from the command line
        Scanner scanner = new Scanner(System.in);

        // Prompt the user to enter their name
        System.out.print("Enter your name: ");
        String name = scanner.nextLine();  // Read user input

        // Prompt the user to enter their age
        System.out.print("Enter your age: ");
        int age = scanner.nextInt();  // Read user input

        // Print a greeting message
        System.out.println("Hello, " + name + "! You are " + age + " years old.");

        // Close the scanner to free resources
        scanner.close();
    }
}

```

[[Notes from Georg]]
This needs to now integrate a [[Connect to database| database connection class]] and [[JDBC| DB class]] 

```java
// Introduce the scanner tool used for reading user input
import java.util.Scanner;

public class Program {

    public static void main(String[] args) {
        // Create a tool for reading user input and name it scanner
        Scanner scanner = new Scanner(System.in);

        // Print "Write a message: "
        System.out.println("Write a message: ");

        // Read the string written by the user, and assign it
        // to program memory "String message = (string that was given as input)"
        String message = scanner.nextLine();

        // Print the message written by the user
        System.out.println(message);
    }
}
```

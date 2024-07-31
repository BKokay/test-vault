---
created: 2024-07-30T13:23
updated: 2024-07-31T12:01
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
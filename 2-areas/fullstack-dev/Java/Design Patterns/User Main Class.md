---
created: 2024-08-02T11:02
updated: 2024-08-02T11:05
---
# Main Class
```java
public class Main {
    public static void main(String[] args) {
        Connection connection = // Initialize your database connection here
        UserDAO userDAO = new UserDAOImpl(connection);
        UserService userService = new UserService(userDAO);

        // Create a new user
        User newUser = new User(1, "John", "Doe", "john@example.com");
        userService.createUser(newUser);

        // Get a user by ID
        User retrievedUser = userService.findUser(1);
        System.out.println(retrievedUser);

        // Update a user
        retrievedUser.setEmail("newemail@example.com");
        userService.modifyUser(retrievedUser);

        // Delete a user
        userService.removeUser(1);
    }
}

```
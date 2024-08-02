---
created: 2024-08-02T11:01
updated: 2024-08-02T11:05
---
# Service Class
```java
import java.util.List;

public class UserService {
    private UserDAO userDAO;

    public UserService(UserDAO userDAO) {
        this.userDAO = userDAO;
    }

    public void createUser(User user) {
        userDAO.addUser(user);
    }

    public User findUser(int id) {
        return userDAO.getUser(id);
    }

    public List<User> getAllUsers() {
        return userDAO.getAllUsers();
    }

    public void modifyUser(User user) {
        userDAO.updateUser(user);
    }

    public void removeUser(int id) {
        userDAO.deleteUser(id);
    }
}

```

[[service class]]
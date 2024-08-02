---
created: 2024-08-02T11:00
updated: 2024-08-02T11:05
---
# DAO Interface
```java
import java.util.List;

public interface UserDAO {
    void addUser(User user);
    User getUser(int id);
    List<User> getAllUsers();
    void updateUser(User user);
    void deleteUser(int id);
}

```

[[DAO Design Pattern]]
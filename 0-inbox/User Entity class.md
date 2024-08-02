---
created: 2024-08-02T10:59
updated: 2024-08-02T11:05
---
# Entity class
```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.Table;
import javax.persistence.Column;

@Entity
@Table(name = "users")
public class User {
    @Id
    @Column(name = "id")
    private int id;

    @Column(name = "first_name")
    private String firstName;

    @Column(name = "last_name")
    private String lastName;

    @Column(name = "email")
    private String email;

    // Getters and Setters
    // Constructors
    // toString, equals, and hashCode methods
}
```

[[entity classes]] 
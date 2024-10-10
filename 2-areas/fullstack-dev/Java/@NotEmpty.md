@NotEmpty validation makes sure that the input is not null and that it is also not an empty string. Can be used in addition to @Size to further give constraints:
```java
@NotEmpty(message = "Name may not be empty")
@Size(min = 2, max = 32, message = "Name must be between 2 and 32 characters long") 
private String name;
```
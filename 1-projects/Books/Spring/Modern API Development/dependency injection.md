Dependency Injection is a specific form of IoC where dependencies are provided to a class from the outside rather than being created inside the class, typically through constructor parameters, setter methods, or field injection. 

Three main types of Dependency Injection are:
1. Constructor Injection where the dependencies are provided through constructor
2. Setter injection where dependencies are set through setter methods
3. Field injection where dependencies are injected directly into fields using `@Autowired`

```java
// Without DI:
class UserService {
	private UserRepository userRepository = new UserRepository(); // tightly coupled
}

// With DI: 
class UserService {
	private UserRepository userRepository;

	@Autowired
	public UserService(UserRepository userRepository) {
		this.userRepository = userRepository;
	}
}
```
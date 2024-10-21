# Spring Data JPA Query Method Naming Conventions Cheatsheet

## Basic Structure
`[operation][By][property][condition][ordering]`

- **operation**: The type of query operation (e.g., `find`, `count`, `delete`, `exists`).
- **By**: Used to specify the property you want to filter by.
- **property**: The name of the entity's field.
- **condition**: (Optional) Used to apply comparisons or other conditions (e.g., `GreaterThan`, `LessThan`, `IsNull`).
- **ordering**: (Optional) Specify sorting (e.g., `OrderBy`).

---

## Common Operations
- `findBy`: Retrieves a list of entities that match the criteria.
- `countBy`: Counts entities that match the criteria.
- `existsBy`: Checks if an entity matching the criteria exists.
- `deleteBy`: Deletes entities that match the criteria.

---

## Combining Multiple Properties
- `findByFirstNameAndLastName(String firstName, String lastName)`
- `findByAgeOrFirstName(int age, String firstName)`

---

## Comparisons (Conditions)
- `GreaterThan`: Finds entities where a property is greater than the given value.
- `LessThan`: Finds entities where a property is less than the given value.
- `Between`: Finds entities where a property is between two values.
- `Before` / `After`: Finds entities where a property is before/after a specific value.

### Examples:
```java
findByAgeGreaterThan(int age)
findByAgeLessThan(int age)
findByBirthDateBetween(LocalDate startDate, LocalDate endDate)
findByCreatedAtBefore(LocalDateTime dateTime)
findByCreatedAtAfter(LocalDateTime dateTime)
```

## Null and Not Null checks
- `IsNull`: Finds entities where the property is null.
- `IsNotNull`: Finds entities where the property is not null.
```java
findByFirstNameIsNull()
findByLastNameIsNotNull()
```

## Boolean Properties
- `True`: Finds entities where the boolean property is true.
- `False`: Finds entities where the boolean property is false.
```java
findByActiveTrue()
findByActiveFalse()
```

## String matching
- `Containing`: Finds entities where the string contains the given value (similar to SQL `LIKE %value%`).
- `StartingWith`: Finds entities where the string starts with the given value (similar to SQL `LIKE value%`).
- `EndingWith`: Finds entities where the string ends with the given value (similar to SQL `%value`).
- `Like`: Finds entities using SQL `LIKE` operator with custom patterns.
```java
findByFirstNameContaining(String namePart)
findByLastNameStartingWith(String prefix)
findByEmailEndingWith(String domain)
findByLastNameLike(String pattern)  // Example: "Jo_n" -> matches "John", "Joan"
```

## Ordering Results

- `OrderBy`: Sorts the result by a property in ascending or descending order.
    - `Asc`: Ascending order.
    - `Desc`: Descending order.
```java
findByFirstNameOrderByLastNameAsc(String firstName)
findByAgeOrderByFirstNameDesc(int age)
```

## Counting Entities

- `countBy`: Counts entities matching a specific condition.
```java
countByFirstName(String firstName)
countByAgeGreaterThan(int age)
```

## Checking Existence

- `existsBy`: Returns true if an entity matching the condition exists.
```java
existsByEmail(String email)
existsByUsername(String username)
```

## Deleting Entities

- `deleteBy`: Deletes entities matching the specified condition.
```java
deleteByFirstName(String firstName)
deleteByAgeLessThan(int age)
```

## Complex Query Examples

### 1. Find all users with the last name "Smith" and first name starting with "J":
```java
findByLastNameAndFirstNameStartingWith(String lastName, String firstNamePrefix)
```

### 2. Find all orders placed between two dates, sorted by the order date in descending order:
```java
findByOrderDateBetweenOrderByOrderDateDesc(LocalDate startDate, LocalDate endDate)
```

### 3. Count users older than 18:
```java
countByAgeGreaterThan(int age)
```

### 4. Check if an email exists in the system:
```java
existsByEmail(String email)
```

### 5. Delete all inactive users:
```java
deleteByActiveFalse()

```

# What is a `Pageable` in [[spring]]?
It is an interface which allows for pagination information, allowing you to split large sets of data into smaller, more manageable chunks or "pages". 

### Key Concepts of `Pageable`:

- **Pagination**: Splitting data into pages, with each page containing a limited number of items.
- **Sorting**: Ordering the data based on specified criteria.
- **Page Number & Size**: You specify the **page number** (starting from 0) and the **page size** (number of records per page) to control which part of the data is fetched.

### Common Use Case:

Imagine you have a database table with 10,000 records, and you don't want to return all records in a single response (which would be inefficient and slow). Instead, you can return the data in pages, like **50 records at a time**.

### Example of Using `Pageable` in Spring:

Suppose you have a repository that returns a list of `Driver` objects. You can modify your method to accept a `Pageable` parameter, which will allow you to request paginated results

```java
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.data.jpa.repository.JpaRepository;

public interface DriverRepository extends JpaRepository<Driver, UUID> {
    Page<Driver> findAll(Pageable pageable);
}
```

Here, `findAll(Pageable pageable)` returns a **Page** object, which contains:

- The data for the current page.
- Metadata about the total number of pages and items.

### How to Use `Pageable` in a Controller:
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api/drivers")
public class DriverController {

    @Autowired
    private DriverRepository driverRepository;

    @GetMapping
    public Page<Driver> getAllDrivers(Pageable pageable) {
        return driverRepository.findAll(pageable);
    }
}
```

### Example Request to Fetch Paginated Results:

If you want to fetch the second page of drivers, with each page showing 10 drivers, you can send a request like this:
```
GET /api/drivers?page=1&size=10
```
- `page=1` refers to the second page (Spring's pagination is **0-based**, so page 0 is the first page).
- `size=10` specifies the number of items per page.

You can also sort the results by specifying a sorting parameter:
```
GET /api/drivers?page=0&size=10&sort=lastName,asc
```

This will return the first page, with 10 drivers, sorted by the `lastName` field in ascending order.

### `Page` vs `List`:

- A **`List`** simply holds a collection of objects without any information about pagination.
- A **`Page`** not only contains the current page of data but also includes useful metadata such as:
    - Total number of pages.
    - Total number of elements.
    - Current page number.
    - Whether it's the last page.

### Key Interfaces and Classes:

- **`Pageable`**: The interface that specifies pagination information (like page number and page size).
- **`PageRequest`**: A common implementation of `Pageable` that provides static methods to create instances.
- **`Page`**: The return type that contains both the data and the pagination metadata.
- **`Slice`**: Similar to `Page`, but contains less metadata. Typically used for performance reasons when only the current chunk of data is needed.

### Example: Manually Creating a `Pageable`

You can manually create a `Pageable` object using `PageRequest`:
```java
import org.springframework.data.domain.PageRequest;
import org.springframework.data.domain.Pageable;

Pageable pageable = PageRequest.of(0, 10);  // Page 0, with 10 items per page
```

### Summary:

- **`Pageable`** is used to represent pagination and sorting in Spring.
- It allows you to fetch data in smaller chunks (pages) rather than all at once.
- It makes API responses more manageable and efficient, especially when dealing with large datasets.

By using `Pageable`, you can handle data efficiently in a user-friendly way, while also allowing sorting and filtering capabilities in your APIs.
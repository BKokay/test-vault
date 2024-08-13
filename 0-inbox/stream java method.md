---
created: 2024-08-13T09:36
updated: 2024-08-13T09:43
---
.stream()
### What is a Java Stream?
It is like a conveyor belt in a restaurant's kitchen, where dishes (or data items) are processed one after the other in a streamlined, efficient way. It allows you to convert a collection into a stream, enabling you to apply various operations in a fluent and readable manner. It leaves the original data source unchanged. 

#### Example
If you have a list of customers, you can use a stream to find all customers who have placed more than 5 orders. 
```java
List<Customer> customers = getCustomers();

List<Customer> frequentCustomers = customers.stream()   // Turn on the conveyor belt
    .filter(c -> c.getOrderCount() > 5)                 // Filter station: only customers with more than 5 orders
    .collect(Collectors.toList());                      // Collect the filtered results into a new list

```

[[java]] [[java methods]] [[java-method-references]] [[Java Map Interface]]
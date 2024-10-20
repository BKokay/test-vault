---
created: 2024-08-21T09:24
<<<<<<< HEAD:0-inbox/Exceptions.md
updated: 2024-09-04T08:49
=======
<<<<<<< HEAD:0-inbox/Exceptions.md
updated: 2024-09-23T11:53
=======
updated: 2024-09-10T09:36
>>>>>>> main:2-areas/fullstack-dev/Java/Exceptions.md
>>>>>>> 9bdce39565b602fd1e4387e0e8dddea923455ea8:2-areas/fullstack-dev/Java/Exceptions.md
---
### What are exceptions?
An exception is an event that happens that interrupts the normal flow of an operation. It could be a bug, it could be the database or server being down, it could be a user input error. But, if not handled correctly, they cause the program to crash. 

There are different types of exceptions in [[java]]. 
##### Checked Exceptions:
Checked exceptions are exceptions that must be either caught or declared in the method signature using the `throws` keyword. They are typically exceptions that can be recovered from. *throws* *recoverable*
- `IOException`
	- Thrown when an input or output operation fails, such as reading from a file that doesn't exist. 
	- `FileNotFoundException` `EOFException`
- `SQLException`
	- Thrown when there is an error interacting with a database, such as when a query is invalid or a connection fails
- `JSONException`
- `NullPointerException`
- `IllegalArgumentException`
	- Thrown to indicate that a method has been passed an illegal or inappropriate argument
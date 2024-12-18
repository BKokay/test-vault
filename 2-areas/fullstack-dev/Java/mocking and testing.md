---
created: 2024-09-02T11:56
<<<<<<< HEAD:0-inbox/mocking and testing.md
updated: 2024-09-04T08:49
=======
updated: 2024-09-23T11:57
>>>>>>> 9bdce39565b602fd1e4387e0e8dddea923455ea8:2-areas/fullstack-dev/Java/mocking and testing.md
---

# What is it?

Testing the functionality of a class without testing its dependencies. Therefore, we need to provide an **object-under-test** which is a replacement for the dependencies which we can control. For example, we might want to force extreme return values, exception throwing or other time-consuming methods in order to get a fixed return value. This controlled replacement is the **mock**.

## Concepts and definitions

- **Dummy** objects are passed around but never actually used. Usually, they are just to fill parameter lists.
- **Fake** objects have working implementations but usually take some shortcuts that make them not suitable for production (an in-memory database, for example using [[H2]])
- **Stubs** provide canned answers to calls made during the test, usually not responding to anything at all outside what's programmed in the test. They can also record info about calls, ie how many responses it sent or something
- **Mocks** are objects pre-programmed with expectations that form a specification of the calls they are expected to receive.

### Format for testing:

```java
@Test
void someVerySpecificName(){
	//given

	//when

	//then
}
```

tools that are used to test [[java]] code:
[[jUnit]]
[[mockito]]
[[jMock]]
[[AssertJ]]

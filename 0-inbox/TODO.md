---
created: 2024-08-29T15:16
updated: 2024-09-04T14:50
---

[[Notes from Georg]] [[Questions 1]]

- [x] add the get extra method to doGet
- [x] Finish making DriverServlet.
- [x] Make device and fuelstop servlet to use in testing
- [x] Test locally
- [x] add db class to mock
- [x] populate test db with data
- [ ] Test
- [ ] think about reducing duplicate code

Where am I? Trying to learn about database testing/mocking. It seems that actually creating a table in Postgres will be best and then tearing it down after doing the tests. The use JUnit to run the tests. But there are so so many options, I feel lost.

To make sure that @beforeall and @afterall gets called, I should extend the db method with each test. Is that the best way? And, also, Springboot will include all of the testing stuff I need. Should I just include it now? No, I think its best to keep doing it in steps so I can see what is happening. Should each test have their own class, or should I make one test for each method?

~~When setting up the doGet method in DriverServlet, I realized that the service.getSavings() method isn't right. I should change that to be getYearlySavings and getMonthlySavings~~
~~I could make the parameter month & year, just like in getYearlySpending/getMonthlySpending. Therefore there would be less room for user error.~~

~~Then I could change the method to be getDriverFinancials(int id, enum Financials, int year, Optional<int> month) only have one DriverFinancialsDTO~~  
~~It would look something like the example in this link: https://favtutor.com/blogs/java-optional-parameters~~

```java
// importing optional class
import java.util.Optional;
// java main class
public class Main{
		// java main method
 		public static void main(String args[]){
			// calling function with all arguments
			System.out.println("Calling the function with all parameters!!");
        	Info("Anubhav","Agrawal",19);
			// calling function without optional parameters
			System.out.println("Calling the function without the optional parameter!!");
			Info("Anubhav",null , 19);
    }
	// user defined method of type Info
    private static void Info(String fname, String lName, int age){
		// creating optional object
		// and making our argument lastname as optional
        Optional lname = Optional.ofNullable(lName);
		// checking if the optional parameter is provided or not
        String optionalParameter = lname.isPresent() ? lname.get() : "Last name not given!";
		// printing out the information
        System.out.println("First Name : "+fname + "\nLast Name : "+optionalParameter +"\nThe age : "+age);
```

Also, I am going to change it to getDriverFinancialSummary(int it, int year, Optional<int> month)

---
created: 2024-08-29T15:16
updated: 2024-09-02T11:48
---
- [x] add the get extra method to doGet
- [x] Finish making DriverServlet. 
- [ ] Make device and fuelstop servlet to use in testing
- [ ] Test locally
- [ ] add db class to mock
- [ ] Test
- [ ] think about reducing duplicate code

When setting up the doGet method in DriverServlet, I realized that the service.getSavings() method isn't right. I should change that to be getYearlySavings and getMonthlySavings 
I could make the parameter month & year, just like in getYearlySpending/getMonthlySpending. Therefore there would be less room for user error. 

Then I could change the method to be getDriverFinancials(int id, enum Financials, int year, Optional<int> month) only have one DriverFinancialsDTO  
It would look something like the example in this link: https://favtutor.com/blogs/java-optional-parameters 
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
##### First: FuelStop
- [x] Update enum for fueltype
- [x] Update tests
- [ ] Make numberOfLiters and int instead of double
	- [ ] I don't think this makes sense for forward compatibility 
- [x] Make sure the enum argument is converted to uppercase
- [x] Update the dbsetup doc with the changes
##### Second: 
- [x] Add timestamp automatically on the java side
##### Third: 
- [x] Update coordinate object to use lat/lon rather than latitude/longitude to be consistent with Server Api. 
- [x] Update gas station classes to reflect these changes
- [x] Update gas station model and class so that name can be null
- [x] Update dbsetup with the change
##### Fourth: 
- [ ] Catch the `HttpMediaTypeNotSupportedException` in the Exception handler class
- [ ] Update all tests to reflect changes
- [x] jar:file:/C:/Users/Keith/.m2/repository/org/json/json/20240303/json-20240303.jar!/org/json/JSONObject.class
	jar:file:/C:/Users/Keith/.m2/repository/com/vaadin/external/google/android-json/0.0.20131108.vaadin1/android-json-0.0.20131108.vaadin1.jar!/org/json/JSONObject.class
##### Fifth:
- [ ] set up logging so that all package errors goes to the normal application log but any spring related errors go to a spring log
##### Sixth:
- [ ] Refactor to use [[Zalando ProblemDetail]] for error handling

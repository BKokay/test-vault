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
- [ ] Update coordinate object to use lat/lon rather than latitude/longitude to be consistent with Server Api. 
- [ ] Update gas station classes to reflect these changes
- [ ] Update gas station model and class so that name can be null
- [ ] Update dbsetup with the change
##### Fourth: 
- [ ] Catch the `HttpMediaTypeNotSupportedException` in the Exception handler class
- [ ] Update all tests to reflect changes

##### Fifth:
- [ ] Refactor to use [[Zalando ProblemDetail]] for error handling

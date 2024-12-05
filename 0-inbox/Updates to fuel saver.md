##### First:
- [ ] Update enum for fueltype
- [ ] Make sure the enum argument is converted to uppercase
- [ ] Update the dbsetup doc with the changes
##### Second: 
- [ ] Add timestamp automatically on the java side
##### Third: 
- [ ] Update coordinate object to use lat/lon rather than latitude/longitude to be consistent with Server Api. 
- [ ] Update gas station classes to reflect these changes
- [ ] Update gas station model and class so that name can be null
- [ ] Update dbsetup with the change
##### Fourth: 
- [ ] Catch the `HttpMediaTypeNotSupportedException` in the Exception handler class
- [ ] Refactor to use [[Zalando ProblemDetail]] for error handling

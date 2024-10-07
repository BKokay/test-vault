## Time Block 10/7
- [ ] 9:10 - 12:00 add logs to each methods
	- [ ] Check how Georg uses logging in the Server API
	- [ ] Refactor controller to only call the service
		- [ ] remove all business logic from controller into service class
			- [ ] actually keep if/else in controller & return ResoibseEntity
				- [ ] in Service, return object
		- [ ] add logging to service class
	- [ ] *Where to put the FuelType enum class?*
	- [ ] *Rename entity to model?*
	- [ ] *Remove CheckInputsUtil and add spring annotations* 
		- [ ] [[@NotNull]]
		- [ ] [[@NotEmpty]]
		- [ ] [[@NotBlank]]
- [ ] 1 - 3 see what kind of errors could be thrown from each layer (use AI)
	- [ ] make sure each error is handled in controller
- [ ] Throughout - Add GOOD comments to explain what each layer or method is doing 

## Time Block 10/8
- [ ] Finish any of the above 
- [ ] Add CI/CD to get it on to staging server
	- [ ] Check properties
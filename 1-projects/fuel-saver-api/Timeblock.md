## 10/8
- [ ] 9:10 - 12:00 add logs to each methods
	- [x] Check how Georg uses logging in the Server API
	- [x] Refactor controller to only call the service
		- [x] remove all business logic from controller into service class
			- [x] actually keep if/else in controller & return ResoibseEntity
				- [x] in Service, return object
		- [x] add logging to service class
	- [x] *Where to put the FuelType enum class?*
	- [ ] *Rename entity to model?*
	- [x] *Remove CheckInputsUtil and add spring annotations* 
		- [x] [[@NotNull]]
		- [x] [[@NotEmpty]]
		- [x] [[@NotBlank]]
- [x] 1 - 3 see what kind of errors could be thrown from each layer
	- [x] make sure each error is handled in controller
- [x] Throughout - Add better comments to explain what each layer or method is doing 
// return the optional from DAO & 404 from this class
// Helper class to not have to repeat over and over
// move back to controller bc controller handles API level so exceptions and
// results
// 1 return object
// 2 exception - 500, 400 (exception handler class)
// 3 empty bc uuid doesnt exist

## 10/11
- [x] Finish any of the above 
- [x] Add CI/CD to get it on to staging server
	- [x] Check properties

## 10/14
- [x] 11-12:30 Finish implementing coordinate in gas station
- [x] 12:30-1 Meditate
- [x] 1-1:30 Read article that Georg sent
- [x] 1:30-3 fix any errors from the tool Georg sent
- [ ] 
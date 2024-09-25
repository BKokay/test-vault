---
created: 2024-09-20T10:39
updated: 2024-09-25T20:58
---
[[springboot]] [[spring]]

*ResponseEntity* represents the whole HTTP response: status code, headers, and body. We can use it to configure the entire HTTP response from our API.

```java
@GetMapping("/age)
public ResponseEntity<String> age(@RequestParam("yearOfBirth) int yearOfBirth) {
	if(isInFuture(yearOfBirth)){
		return new ResponseEntity<>("Year of birth cannot be in future", HttpStatus.Bad_Request);
	}

	return new ResponseEntity<>("Your age is " + calculateAge(yearOfBirth), HttpStatus.OK);
}			
```
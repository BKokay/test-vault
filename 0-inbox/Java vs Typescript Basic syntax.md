---
created: 2024-07-26T09:52
updated: 2024-07-26T10:09
---
### Numbers
##### JavaScript/TypeScript
```JavaScript
let x: number = 10;
const y: number = 20; 
```

##### Java 
```Java
int x = 10
final int y = 20
```
[[java numbers]] 
### Functions/Methods
##### JavaScript/TypeScript
```JavaScript
function add(a:number,b:number): number{
	return a + b
} 
```

##### Java 
```Java
public int add(int a, int b){
	return a + b
}

//public = type
//int = return type 
//add = function name
//int a, int b = tells you what the type of the argument must be 
```
[[java methods]]

### Classes and Objects
##### JavaScript/TypeScript
```JavaScript
class Person{
	name: string;

	constructor(name: string){
		this.name = name;
	}

	greet(): void {
		console.log(`Hello, my name is ${this.name})
	}
}

let person = new Person("John");
person.greet()
```

##### Java 
```Java
public class Person {
	private String name;

	public Person(String name){ //this is the constructor
		this.name = name;
	}

	public void greet() {
		System.out.println("Hello, my name is " + this.name);
	}

	public static void main(String[] args){ //the main is what runs when the program is called
		Person person = new Person("John");
		person.greet();
	}
}
```
[[java classes]] #check


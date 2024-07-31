---
created: 2024-07-31T11:12
updated: 2024-07-31T11:21
---
It is an [[java annotation | annotation]] that is use to indicate that a method is intended to override a method in a superclass. 

### Key Purposes of `@Override`

1. **Ensures Correct Method Signature**:
    
    - When you use `@Override`, the compiler checks that the method actually overrides a method in its [[superclass]]. If you make a mistake in the method signature (e.g., a typo in the method name, wrong parameter types), the compiler will generate an error.
    - Without `@Override`, the compiler won't flag the mistake, and you might end up creating a new method instead of overriding the intended one.
2. **Improves Code Readability**:
    
    - It makes the code more understandable by explicitly indicating that the method is overriding a method from the superclass. This can be especially helpful when maintaining or debugging code.
3. **Prevents Accidental Overloading**:
    
    - If you intend to override a method but accidentally change the method signature (such as changing a parameter type), using `@Override` will prevent [[accidental overloading]].

#### Example of `@Override`
```java
class Animal {
	public void sound(){
		System.out.println("Animal makes a sound");
	}
};

//incorrect Override of the Animal class
//Complier will produce an error b/c there is no method called sounds() in the Animal superclass to override
class Dog extends Animal {
	@Override 
	public void sounds(){
		System.out.println("Dog barks");
	}
};
//Correct and program will compile
class Dog extends Animal {
	@Override 
	public void sound(){
		System.out.println("Dog barks");
	}
};
```
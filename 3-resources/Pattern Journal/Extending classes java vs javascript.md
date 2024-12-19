Java and JavaScript both can extend classes. How are they different? 

[[java]] uses two keywords: `extends` & `implements`. When you extend a class, you inherit all of its methods. You can override them, or just leave them as is. When you implement a class, you must implement all of the methods with the same return and parameter type as defined in the interface you extended. A java class can implement multiple classes but extend just one. 
![[Pasted image 20241219110706.png]]

Example: 
```java
interface Animal {
    void makeSound();
}

class Mammal {
    void breathe() {
        System.out.println("Breathing...");
    }
}

class Dog extends Mammal implements Animal {
    @Override
    public void makeSound() {
        System.out.println("Bark!");
    }
}
```

Similarly, [[javascript]] supports single class inheritance. The constructor is automatically inherited unless you want to change it using [[Super in java vs javascript| super]]. 
```javascript
class Animal {
    constructor(name) {
        this.name = name;
    }

    makeSound() {
        console.log(`${this.name} makes a sound`);
    }
}

class Dog extends Animal {
    makeSound() {
        console.log(`${this.name} barks`);
    }
}

const dog = new Dog('Buddy');
dog.makeSound(); // Outputs: Buddy barks

```

Javascript does not have the `implements` keyword although there are workarounds. 

The main difference is that JavaScript classes are just syntactic sugar over prototypal inheritance from JS before the introduction of classes. 
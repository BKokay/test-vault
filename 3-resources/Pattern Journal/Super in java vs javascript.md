The keyword `super` is different in [[java]] vs [[javascript]] although they share some similarities.

## Java
In java, `super` is used to access a parent methods fields, methods, or constructors. 
### access a parent's fields
To access a parent's fields, you can use `super` if the child has a field with the same name. 
```java
class Animal {
    String sound = "Generic animal sound";
}

class Dog extends Animal {
    String sound = "Bark";

    void printSounds() {
        System.out.println("Child class sound: " + sound);
        System.out.println("Parent class sound: " + super.sound);
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.printSounds();
    }
}
```

### access a parent's methods that have already been overridden 
```java 
class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Dog barks");
    }

    void callParentSound() {
        super.makeSound(); // Calls the parent class method
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.makeSound();       // Outputs: Dog barks
        dog.callParentSound(); // Outputs: Animal makes a sound
    }
}
```

### calling a parent classes constructor

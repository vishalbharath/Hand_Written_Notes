-  **abstraction** is the process of hiding certain details and showing only essential information to the user.
- can be achieved with either **abstract classes** or interfaces
- The `abstract` keyword is a non-access modifier
- **Example**: You drive a car without knowing how the engine works internally  you just use the steering, pedals, etc.

#### Abstract Classes
-  class that can not be instantiated by itself (Can't create object )
- it needs to be subclassed by another class to use its properties.
-  declared using the "abstract" keyword
- Main things to be notes in Abstract Classes
  -  An instance of an abstract class can not be created.
  -  Constructors are allowed.
  -  We can have an abstract class without any abstract method.
  - There can be a ****final method**** in abstract class but any abstract method in class
  -  We can define static methods in an abstract class

#### Abstract Methods
- An **abstract method** is a method that **has no body**
- declared using the `abstract` keyword
- Subclasses must provide an implementation for it.
- does not have a body
- The body is provided by the subclass

```java
// Abstract class
abstract class Animal {
    String name;

    // Abstract method
    abstract void makeSound();

    // Concrete method
    void printName() {
        System.out.println("Animal name is: " + name);
    }
}

// Subclass providing implementation
class Dog extends Animal {

    // Constructor
    Dog(String n) {
        name = n;  // Setting the name directly, no 'this'
    }

    // Implementing abstract method
    void makeSound() {
        System.out.println("Dog barks: Woof Woof!");
    }
}

// Another subclass
class Cat extends Animal {

    Cat(String n) {
        name = n;
    }

    void makeSound() {
        System.out.println("Cat meows: Meow Meow!");
    }
}

// Main class to test
public class Main {
    public static void main(String[] args) {
        Dog d = new Dog("Buddy");
        d.printName();
        d.makeSound();

        Cat c = new Cat("Whiskers");
        c.printName();
        c.makeSound();
    }
}
```
```


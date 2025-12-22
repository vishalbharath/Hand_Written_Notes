-  Single Inheritance
- Multilevel Inheritance
- Hierarchical Inheritance
- Multiple Inheritance (not supported in Java)
- Hybrid Inheritance

#### Single Inheritance
- a sub-class is derived from only one super class
-  It inherits the properties and behavior of a single-parent class also known as simple inheritance.
![[Pasted image 20250714204355.png]]

==Example
```java
// Java program to illustrate the
// concept of single inheritance
import java.io.*;
import java.lang.*;
import java.util.*;

// Parent class
class One {
    public void print_animal()
    {
        System.out.println("dog");
    }
}

class Two extends One {
    public void print_for() { System.out.println("cat"); }
}

// Driver class
public class Main {
      // Main function
    public static void main(String[] args)
    {
        Two g = new Two();
        g.print_animal();//dog
        g.print_for();//cat
        g.print_animal();//dog
    }
}
```

#### Multi Level Inheritance
-  a derived class will be inheriting a base class, and as well as the derived class
- a class is derived from a class which is already derived from another class.
![[Pasted image 20250716200026.png]]
- ==Example code
```java
// Base class
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

// Derived class (inherits from Animal)
class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks.");
    }
}

// Derived class (inherits from Dog)
class Puppy extends Dog {
    void weep() {
        System.out.println("The puppy weeps.");
    }
}

// Main class to run the program
public class MultilevelInheritanceExample {
    public static void main(String[] args) {
        Puppy myPuppy = new Puppy();

        myPuppy.eat();   // Inherited from Animal (o/p : This animal eats food. )
        myPuppy.bark();  // Inherited from Dog(o/p : The dog barks.)
        myPuppy.weep();  // Own method(o/p: The puppy weeps.)
    }
}

```


#### Hierarchical Inheritance
- one class serves as a superclass (base class) for more than one subclass
- multiple classes inherit from a single parent class.
- multiple classes inherit from a single parent class.
![[Pasted image 20250716200818.png]]

- ==Example code

```java
// Parent class
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

// Child class 1
class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks.");
    }
}

// Child class 2
class Cat extends Animal {
    void meow() {
        System.out.println("The cat meows.");
    }
}

// Main class to run the program
public class HierarchicalInheritanceExample {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        Cat myCat = new Cat();

        // Access methods from parent and child
        myDog.eat();   // From Animal (o/p : This animal eats food.)
        myDog.bark();  // From Dog (o/p : The dog barks.)

        myCat.eat();   // From Animal (o/p : This animal eats food.)
        myCat.meow();  // From Cat (o/p : The cat meows.)
    }
}

```


#### Hybrid Inheritance
- mix of two or more of the above types of inheritance.
- we can achieve hybrid inheritance only through Interfaces.


![[Pasted image 20250731090912.png]]
![[Pasted image 20250731091016.png]]

```java
// Base class
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

// Derived class - Hierarchical inheritance
class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks.");
    }
}

// Another derived class - Hierarchical inheritance
class Cat extends Animal {
    void meow() {
        System.out.println("Cat meows.");
    }
}

// Multilevel inheritance
class Puppy extends Dog {
    void weep() {
        System.out.println("Puppy weeps.");
    }
}

public class HybridInheritanceExample {
    public static void main(String[] args) {
        Puppy p = new Puppy();
        p.eat();   // from Animal
        p.bark();  // from Dog
        p.weep();  // from Puppy

        Cat c = new Cat();
        c.eat();   // from Animal
        c.meow();  // from Cat
    }
}

```


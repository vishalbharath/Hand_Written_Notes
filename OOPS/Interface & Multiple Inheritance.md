- an abstract type used to specify the behaviour of a class
- Another way to achieve abstraction in Java
- By default, variables in an interface are public, static and final.
- used to achieve abstraction and multiple inheritance Java.
- *Think of an interface as a **contract**: any class that implements it **must provide implementations** for its abstract methods.*

```java
// Interface
interface Animal {
    void makeSound();  // abstract method
}

// Class implementing interface
class Dog implements Animal {
    public void makeSound() {
        System.out.println("Dog says: Woof!");
    }
}

// Another class
class Cat implements Animal {
    public void makeSound() {
        System.out.println("Cat says: Meow!");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal d = new Dog();
        Animal c = new Cat();
        
        d.makeSound();  // Output: Dog says: Woof!
        c.makeSound();  // Output: Cat says: Meow!
    }
}

```

#### Multiple Inheritance in Java 
![[Pasted image 20250731102655.png]]

- **Multiple inheritance** means a class can inherit **features (methods)** from **more than one parent**.
```java
// Interface 1
interface Printable {
    void print();
}

// Interface 2
interface Showable {
    void show();
}

// Class implementing both interfaces
class Document implements Printable, Showable {
    public void print() {
        System.out.println("Printing document...");
    }

    public void show() {
        System.out.println("Showing document...");
    }
}

// Main class
public class Main {
    public static void main(String[] args) {
        Document d = new Document();
        d.print();  // Output: Printing document...
        d.show();   // Output: Showing document...
    }
}

```


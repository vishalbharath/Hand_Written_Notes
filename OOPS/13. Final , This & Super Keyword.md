
#### Final Keyword
- a non-access modifier used to prevent modification
- cannot be overridden
-  final prevents its value from being changed after initialization
```java
```java
public class Main {
  final int x = 10;

  public static void main(String[] args) {
    Main myObj = new Main();
    myObj.x = 25; // will generate an error: cannot assign a value to a final variable
    System.out.println(myObj.x);
  }
}
```

#### Super Keyword
- used to refer to the parent class
- It is used to call superclass methods, and to access the superclass constructor.
- used to refer to the immediate parent class of a subclass

```java
// Parent class
class Animal {
    String type = "Animal";

    Animal() {
        System.out.println("Animal constructor called");
    }

    void display() {
        System.out.println("This is an animal");
    }
}

// Child class
class Dog extends Animal {
    String type = "Dog";

    Dog() {
        super(); // Calling parent class constructor
        System.out.println("Dog constructor called");
    }

    void printType() {
        System.out.println("Type in child class: " + type);
        System.out.println("Type in parent class: " + super.type); // Accessing parent class field
    }

    void display() {
        super.display(); // Calling parent class method
        System.out.println("This is a dog");
    }
}

// Main class
public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.printType();
        d.display();
    }
}

```

#### This Keyword
-  refers to the current object
- Call current class methods and fields
- To pass an instance of the current class as a parameter
- To differentiate between the local and instance variables.
- eliminate the confusion between class attributes and parameters with the same name
```java
class Student {
    String name;
    int age;

    // Constructor with parameter names same as instance variables
    Student(String name, int age) {
        this.name = name;  // 'this' differentiates instance variable from parameter
        this.age = age;
    }

    void display() {
        System.out.println("Name: " + this.name); // 'this' refers to the current object
        System.out.println("Age: " + this.age);
    }

    // Method that accepts an object
    void show(Student s) {
        System.out.println("Student info: " + s.name + ", " + s.age);
    }

    // Pass current object as an argument
    void callShow() {
        show(this); // passing current object to another method
    }

    // Returning current object
    Student getStudent() {
        return this;
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student("Alice", 20);
        s1.display();
        s1.callShow();

        Student s2 = s1.getStudent(); // returns the current object
        System.out.println("Returned object name: " + s2.name);
    }
}

```


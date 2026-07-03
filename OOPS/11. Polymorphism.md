-  It Means "Many forms"
- it occurs when we have many classes that are related to each other by inheritance.
```java
```java
class Animal {
  public void animalSound() {
    System.out.println("The animal makes a sound");
  }
}

class Pig extends Animal {
  public void animalSound() {
    System.out.println("The pig says: wee wee");
  }
}

class Dog extends Animal {
  public void animalSound() {
    System.out.println("The dog says: bow wow");
  }
}

class Main {
  public static void main(String[] args) {
    Animal myAnimal = new Animal();  // Create a Animal object
    Animal myPig = new Pig();  // Create a Pig object
    Animal myDog = new Dog();  // Create a Dog object
    myAnimal.animalSound();
    myPig.animalSound();
    myDog.animalSound();
  }
}
```

#### Method Overloading

- occurs when we have multiple methods in the same class with the same name but have different numbers of parameters.
- It allows to perform operations with different inputs.
- also known as ==compile-time polymorphism==
- In method overloading the ==return type of these methods can be same or different==
- does not require inheritance.
-  improves code readability

```java
class Calculator {
    // Method with 2 int parameters
    int add(int a, int b) {
        return a + b;
    }

    // Method with 3 int parameters (Overloaded)
    int add(int a, int b, int c) {
        return a + b + c;
    }

    // Method with double parameters (Overloaded)
    double add(double a, double b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(2, 3));       // 5
        System.out.println(calc.add(2, 3, 4));    // 9
        System.out.println(calc.add(2.5, 3.5));   // 6.0
    }
}

```


#### Method Overriding 
-  occurs when a subclass provides a specific implementation for a method that is already defined in the superclass.
- Method Overriding is a type of ==runtime polymorphism.==
-  a method in a derived class has the same name, return type, and parameters as a method in its parent class
- requires inheritance.
- return type must be same.
- private and final methods can not be overridden.
- @Override annotation ensures correct overriding.

```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {  // Overriding the parent method
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal a1 = new Dog();  // Runtime decision
        Animal a2 = new Cat();

        a1.sound();  // Dog barks
        a2.sound();  // Cat meows
    }
}

```

![[Pasted image 20250714193032.png]]
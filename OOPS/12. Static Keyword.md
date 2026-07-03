-  mainly used for ****memory management****
- ****allowing variables and methods to belong to the class itself rather than individual instances****
- The static keyword belongs to the class rather than an instance of the class
-  static keyword is a ****non-access modifier****
-  used for methods and attributes.
-  can be accessed without creating an object of a class.
- Object create panama method aa access panradhuku static keyword use panrom 
- 

```java
```java
public class Main {
  // Static method
  static void myStaticMethod() {
    System.out.println("Static methods can be called without creating objects");
  }

  // Public method
  public void myPublicMethod() {
    System.out.println("Public methods must be called by creating objects");
  }

  // Main method
  public static void main(String[ ] args) {
    myStaticMethod(); // Call the static method
    // myPublicMethod(); This would output an error

    Main myObj = new Main(); // Create an object of Main
    myObj.myPublicMethod(); // Call the public method
  }
}
```
```


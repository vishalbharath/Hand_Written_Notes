-   It has the same name as the class name .
- The main job is to initialize the objects 
- The constructor is called when an object of a class is created.
- used to set initial values for object attributes.
- A Constructor does not have any return type.
- A Constructor can also take parameters as input and it is said to be parameterized Constructor. 

==Example of an Constructor==

```java
class Sample{
    int rollno;
    String name;
}
class Main{
    public static void main(String[] args){
        Sample obj = new Sample(); // here sample is the constructor as it is the name of the class
        System.out.println(obj.rollno);
        System.out.println(obj.name);
    }
}
```

==Example of a Parameterized Constructor==
```java
class Sample{
    int rollno;
    String name;

	sample(int num , int nam){//this is how the constructor looks like 
		rollno = num;
		name = nam;
	}
}
class Main{
    public static void main(String[] args){
        Sample obj = new Sample(110,"vishal"); // here parameter is passed inside the constructor
        System.out.println(obj.rollno);
        System.out.println(obj.name);
    }
}
```

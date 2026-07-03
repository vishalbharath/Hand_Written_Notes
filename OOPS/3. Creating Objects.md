==Example  :== 
```java
`class AppForm{
    String name;
    int rollno;
    
    public void display(){
        System.out.println(name);
        System.out.println(rollno);
    }
    public static void main(String[] args){
        AppForm vishal = new AppForm(); //class name must be before object name
        vishal.name = "vishal";
        vishal.rollno = 110;
        vishal.display();
    }
}`
```

> AppForm vishal = new AppForm();
> Here AppForm is the class name and vishal is the object name 


==Accessing classes in other classes using object :== 
```java
`class AppForm{`
    `String name;`
    `int rollno;`
    
    `public void display(){`
        `System.out.println(name);`
        `System.out.println(rollno);`
    `}`
`}`
`class Main{`
    `public static void main(String[] args){`
        `AppForm vishal = new AppForm(); //class name must be before object name`
        `vishal.name = "vishal";`
        `vishal.rollno = 110;`
        `vishal.display();`
        
	    `AppForm tino = new AppForm();`
        `tino.name = "tino britty";`
        `tino.rollno = 42;`
        `tino.display();`
    `}`
`}`
```

==Another example of the same with passing Parameters :==
```java
`class AppForm{`
    `String name;`
    `int rollno;`
    
    `public void display(){`
        `System.out.println(name);`
        `System.out.println(rollno);`
    `}`
    
    `public void setValues(String str , int no){`
        `name = str;`
        `rollno = no;`
    `}`
`}`
`class Main{`
    `public static void main(String[] args){`
        `AppForm vishal = new AppForm();` 
        `vishal.setValues("vishal",110); //passing parameters as input to the class` 
        `vishal.display();`
        
        `AppForm tino = new AppForm();`
        `tino.name = "tino britty";`
        `tino.rollno = 42;`
        `tino.display();`
        
        
    `}`
`}`
```


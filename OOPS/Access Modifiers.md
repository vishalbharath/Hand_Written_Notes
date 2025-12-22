There are 3 types of Access modifiers in java 
1) Public
2) Private 
3) Protected

##### 1)Public
		It can be accessed anywhere inside a function and across a function. 
		Example: 
```java
			`class AppForm{
			    String name;
			    int rollno;
    
			public void display(){
		        System.out.println(name);
		        System.out.println(rollno);
			}
    
		    public void setValues(String str , int no){
		        name = str;
		        rollno = no;
		    }
		}
			class Main{
			    public static void main(String[] args){
			    AppForm vishal = new AppForm(); 
		        vishal.setValues("vishal",110);
		        vishal.display();//we used public in display function so that we can access it across other class.
			 }
		}`
```
```

```
##### 2) Private
			It can be accessed only inside the function where it is been declared.
	Example:
```java
	class AppForm{
		    private String name; //here name is declared as private x
		    int rollno;
    
	    public void display(){
	        System.out.println(name);
	        System.out.println(rollno);
	    }
    
	    public void setValues(String str , int no){
	        name = str;
	        rollno = no;
	    }
	}
		class Main{
		    public static void main(String[] args){
		        AppForm vishal = new AppForm(); 
		        vishal.setValues("vishal",110); 
		        vishal.display();//vishal , 110
        
		        AppForm tino = new AppForm();
		        tino.name = "tino britty";//error: name has private access in AppForm
		        tino.rollno = 42;//42
		        tino.display();
        
        
    }
}
```


			From the above example we can see that when we use name as private in AppForm class we cannot access it directly it in the Main class.

				but when we use a set function to accesing the name it is not showing an error as the set function is declared in AppForm class so while accessing the set function we dont get any error .

					From this we can say that when we use private we can't access it directly, we can access it only by using a setter or getter function . 


##### 3) Protected
It is same as public . the main difference is that when we use protected we cant access the variables or methods in other packages.
also we cannot access it in the inherited classes.

	




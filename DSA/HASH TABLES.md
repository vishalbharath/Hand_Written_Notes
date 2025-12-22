-  A **Hash Table** is a data structure that stores **key–value pairs**
-  It is similar to HashMap, but is synchronized.
- allows for very fast data retrieval, insertion, and deletion
- typically in **O(1)** average time.
- A hash table uses a **hash function** to convert a key into an **index** (also called a hash code)
- The key doesn’t directly tell us where data is stored — the hash function decides that.
- This is why you can retrieve values quickly **without scanning the whole table**.


 ##### *HOW IT WORKS* 
 - **Insert**:
    - Take the key → apply hash function → get an index.
    - Store the key–value pair at that index.
- **Search**:
    - Take the key → apply the same hash function → find the index → return value.
- **Delete**:
    - Locate using the hash function → remove the pair.

![[Pasted image 20250810141110.png]]
- In The Below Example the Entry is an Integer and a String 
![[Pasted image 20250810141154.png]]

- In the Below Example Both the Entry is Strings 
![[Pasted image 20250810141429.png]]

 Hashtable = A data structure that stores unique keys to values ex.<Integer, String>
	    	   Each key/value pair is known as an Entry
FAST insertion, look up, deletion of key/value pairs
Not ideal for small data sets, great with large data sets
    	
hashing = Takes a key and computes an integer (formula will vary based on key & data type)
In a Hashtable, we use the hash % capacity to calculate an index number 
    	
key.hashCode() % capacity = index  
    	
bucket = an indexed storage location for one or more Entries
can store multiple Entries in case of a collision (linked similarly a LinkedList)
    	
collision = hash function generates the same index for more than one key
    			less collisions = more efficiency
    	
Runtime complexity: Best Case O(1)
    	                Worst Case O(n)
    	
```java
import java.util.*;

public class Main{
	
    public static void main(String args[]) {    	
    	Hashtable<Integer, String> table = new Hashtable<>(10);
    	
    	table.put(100, "Spongebob");
    	table.put(123, "Patrick");
    	table.put(321, "Sandy");
    	table.put(555, "Squidward");
    	table.put(777, "Gary");
    	  	
    	for(Integer key : table.keySet()) {
    		System.out.println(key.hashCode() % 10 + "\t" + key + "\t" + table.get(key));
    	}
    }
}
```
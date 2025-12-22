## Scanner
```java
Scanner sc = new Scanner(System.in);

while (sc.hasNext()) {
	String input = sc.next();
	list.add(input);
}
```
## HashMap
```java
// Creation:
HashMap<Integer, Integer> a = new HashMap<>();

// Frequency finding
for(int i : nums) {
    a.put(i, a.getOrDefault(i, 0) + 1);
}

capitalCities.put("England", "London");
capitalCities.get("England");
capitalCities.remove("England");
capitalCities.size();

capitalCities.containsKey("Londom"));
capitalCities.containsValue("Geeks"));
// Print keys
for (String i : capitalCities.keySet()) {
  System.out.println(i);
}

// Print values
for (String i : capitalCities.values()) {
  System.out.println(i);
}

// Print keys and values
for (String i : capitalCities.keySet()) {
  System.out.println("key: " + i + " value: " + capitalCities.get(i));
}

// forEach()
a.forEach((key, value) -> {
  value = value - 10;
  System.out.print("hello",value);  
});
```

```java
a.keySet()        // Returns a set of key values
int f = a.get(i); // Returns the value at key i;
```


## Hashset
```java
HashSet<String> cars = new HashSet<String>();

cars.add("Volvo");
cars.add("BMW");
cars.contains("Mazda"); // Check if an item exists
cars.remove("Volvo"); // Remove an Item
cars.size();

// Loop through
for (String i : cars) {
  System.out.println(i);
}

```
## Sieve of Eratosthenes
- For Finding primes
```java
class Solution {
    public int countPrimes(int n) {
        int count = 0;
        boolean[] arr = new boolean[n];
        for(int i=0; i<n; i++) {
           arr[i] = true; 
        }
		
        for(int i = 2; i*i < n; i++) {
            if(arr[i]) {
                for(int j=i*i; j < n; j+=i) {
                    arr[j] = false;
                }
            }
        }
		
        for(int i = 2; i < n; i++) {
            if(arr[i]) {
                count++;
            }
		}
	       
       return count;
    }
}
```

## ArrayList
```java
ArrayList<Integer> arr2 = new ArrayList<Integer>();

java.u­til.Ar­rayList Methods

l.add(itm)  //Add itm to list
l.get(i)  //Return ith item
l.size()  //Return number of items
l.remove(i)  //Remove ith item
l.set(i, val)  //Put val at position i

l.contains(5);
l.size();


// Reverse a array list
Collections.reverse(l);

 arr1.add(i);
 arr.get(2);
 
// using IndexOf() to find first index of 6 
int pos1 =arr.indexOf(6); 

// using lastIndexOf() to find last index of 6 
int pos2 =arr.lastIndexOf(6); 
```

## String
```java
myStr.indexOf("e", 5)
s1.equals(s2)
"AB".equalsIgnoreCase("ab")


str.toUpperCase();     // ABCD
str.toLowerCase();     // abcd
str.concat("#");       // Abcd#
str.replace("b", "-"); // A-cd

"  abc ".trim();       // abc

String str = "abcd";
str.charAt(2);       // c
str.indexOf("a")     // 0
str.indexOf("z")     // -1
str.length();        // 4
str.toString();      // abcd
str.substring(2);    // cd
str.substring(2,3);  // c
str.contains("c");   // true
str.endsWith("d");   // true
str.startsWith("a"); // true
str.isEmpty();       // false

a = a.replaceAll(" ","");
if( i.matches("[0-9]+")){
	al.add(Integer.parseInt(i));
}

// String to Char Array
str.toCharArray()
```

## String Builder
```java
StringBuilder sb = new StringBuilder();

sb.append(carry % 2);
sb.delete(5, 9);
sb.insert(0, "My ");

sb.reverse().toString()
```

## Imports
```java
import java.lang.Math;
import java.util.Scanner;
```

## Array
```java
int[] arr = new int[5]; 
arr.length

Arrays.toString(intArr));
```



---
## Sujeeth
```java
import java.util.ArrayList;
import java.util.Scanner;

class A {
    public static void main(String args[]) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter an array (e.g., [1, 2, 3]):");
		
        String input = scanner.nextLine(); // Read the input line
        input = input.replaceAll("\\[|\\]|\\s", ""); // Remove brackets and whitespace
		
        String[] elements = input.split(","); // Split the input string by commas
        ArrayList<Integer> arrayList = new ArrayList<>(); // Create an ArrayList to store the elements
		
        for (String element : elements) {
            if (!element.isEmpty()) {
                arrayList.add(Integer.parseInt(element)); // Parse each element as an integer and add to the list
            }
        }
		
        // Convert the ArrayList to an array if needed
        int[] array = arrayList.stream().mapToInt(Integer::intValue).toArray();
		
        // Output the array
        System.out.println("The array is:");
        for (int num : array) {
            System.out.print(num + " ");
        }
    }
}
```

```java
class Solution {
    public int[] singleNumber(int[] nums) {
        Integer[] ab=Arrays.stream(nums).boxed().toArray(Integer[]::new);
        List<Integer> arr= Arrays.asList(ab);
        Set<Integer> harr=new HashSet<>(arr);
        int a[]=new int[2];
        int k=0;
        for(int j : harr)
        {
            int i=Collections.frequency(arr,j);
            if(i==1)
            {
                a[k]=j;
                k++;
            }
            if(k>1)
            {
                break;
            }
        }
        return a;
    }
}
```


---
## Sutheeb
```java
import java.util.*;

class Solution {
    public static void main(String[] args) {
        Scanner r = new Scanner(System.in);
        ArrayList<Integer> nums = new ArrayList<>();
        
        // Read integers until a non-integer is entered
        while (r.hasNextInt()) {
            int num = r.nextInt();
            nums.add(num);
        }
        
        r.close();  // Close the scanner as it is no longer needed

        // Sort the list
        Collections.sort(nums);

        // Create a new list to store unique elements
        ArrayList<Integer> uniqueNums = new ArrayList<>();

        // Iterate through the sorted list to find unique elements
        for(int i = 0; i < nums.size(); i++) {
            if(i < nums.size() - 1 && nums.get(i).equals(nums.get(i + 1))) {
                i++;  // Skip the next element as it is the same
            } else {
                uniqueNums.add(nums.get(i));  // Add the unique element to the new list
            }
        }

        // Convert the uniqueNums list to an array
        int[] result = new int[uniqueNums.size()];
        for(int i = 0; i < uniqueNums.size(); i++) {
            result[i] = uniqueNums.get(i);
        }

        // Print the unique elements
        System.out.println("Unique elements are: " + Arrays.toString(result));
    }
}




import java.util.*;

class Solution {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter a string to check if it is a palindrome:");
        String input = scanner.nextLine();
        scanner.close();  // Close the scanner as it is no longer needed

        // Process the input string
        String cleanedInput = input.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();

        // Check if the processed string is a palindrome
        boolean isPalindrome = isPalindrome(cleanedInput);

        // Print the result
        if (isPalindrome) {
            System.out.println("The string is a palindrome.");
        } else {
            System.out.println("The string is not a palindrome.");
        }
    }

    public static boolean isPalindrome(String str) {
        int left = 0;
        int right = str.length() - 1;

        while (left < right) {
            if (str.charAt(left) != str.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }

        return true;
    }
}




import java.util.*;
public class Solution {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter a string:");
        String s = scanner.nextLine();
        scanner.close();  // Close the scanner as it is no longer needed

        String longestPalindrome = longestPalindrome(s);
        System.out.println("The longest palindromic substring is: " + longestPalindrome);
    }

    public static String longestPalindrome(String s) {
        if (s == null || s.length() < 1) {
            return "";
        }
        int start = 0, end = 0;
        for (int i = 0; i < s.length(); i++) {
            int len1 = expandAroundCenter(s, i, i);
            int len2 = expandAroundCenter(s, i, i + 1);
            int len = Math.max(len1, len2);
            if (len > end - start) {
                start = i - (len - 1) / 2;
                end = i + len / 2;
            }
        }
        return s.substring(start, end + 1);
    }

    private static int expandAroundCenter(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        return right - left - 1;
    }
}
```

---
## Collections
```java
Collections.addAll(items, "Fruits", "Bat", "Ball"); 

Collections.sort(items, Collections.reverseOrder());
Collections.binarySearch(items, "Horse")); 


```


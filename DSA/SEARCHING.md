
### LINEAR SEARCH 

![[Pasted image 20250807093001.png]]
- It works by **checking each element in the array one by one** until the target element is found or the end of the array is reached.
##### When to Use Linear Search
- When the data is **unsorted**
- When the dataset is **small**
- When you want **simple logic**

```java
public class LinearSearchExample {
    
    // Linear Search Method
    public static int linearSearch(int[] arr, int target) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == target) {
                return i; // target found, return index
            }
        }
        return -1; // target not found
    }

    public static void main(String[] args) {
        int[] numbers = {5, 2, 9, 1, 7, 6};
        int target = 7;

        int index = linearSearch(numbers, target);

        if (index != -1) {
            System.out.println("Element found at index: " + index);
        } else {
            System.out.println("Element not found in the array.");
        }
    }
}

```

![[Pasted image 20250807100829.png]]

### BINARY SEARCH 

- **Binary Search** is an efficient algorithm used to **search for a target element in a sorted array
- The array **must be sorted**
- Faster than linear search for large datasets

**Steps:**

1. Start with the left and right bounds (`left = 0`, `right = n - 1`)
2. Find the middle index:  
    `mid = (left + right) / 2`
3. Compare `arr[mid]` with the target:
    - If equal → return `mid`
    - If target < `arr[mid]` → search the **left half**
    - If target > `arr[mid]` → search the **right half**
4. Repeat steps 2–3 until the element is found or bounds cross.

```java 
public class BinarySearchExample {

    // Binary Search Method (Iterative)
    public static int binarySearch(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2; // avoid overflow

            if (arr[mid] == target) {
                return mid; // target found
            } else if (arr[mid] < target) {
                left = mid + 1; // search right half
            } else {
                right = mid - 1; // search left half
            }
        }

        return -1; // not found
    }

    public static void main(String[] args) {
        int[] sortedArr = {1, 3, 5, 7, 9, 11, 13, 15};
        int target = 9;

        int index = binarySearch(sortedArr, target);

        if (index != -1) {
            System.out.println("Element found at index: " + index);
        } else {
            System.out.println("Element not found.");
        }
    }
}

```

![[Pasted image 20250807100816.png]]

#### INTERPOLATION SEARCH 
 - **Interpolation Search** is an improvement over **Binary Search** for **uniformly distributed** sorted data.  
- Instead of always choosing the middle element, it **guesses the likely position** of the target using the formula of linear interpolation.

 ### When to Use Interpolation Search
- The array must be **sorted**.
- The data should be **uniformly distributed** (e.g., 10, 20, 30, 40…).
- You're looking for **more efficient searching** than binary search in such cases.

- Formula 
		int pos = low + (high - low) * (target - array[low]) / 
			        (array[high] - array[low]);


```java
public class InterpolationSearchExample {

    // Interpolation Search Method
    public static int interpolationSearch(int[] arr, int target) {
        int low = 0, high = arr.length - 1;

        while (target >= array[low] && target<= array[high] && low<= high) {

            // Estimate the position of target
            int pos = low + (high - low) * (target - array[low]) / 
			        (array[high] - array[low]);


            if (arr[pos] == target)
                return pos;
            else if (arr[pos] < target)
                low = pos + 1;
            else
                high = pos - 1;
        }

        return -1; // Not found
    }

    public static void main(String[] args) {
        int[] sortedArr = {10, 20, 30, 40, 50, 60, 70, 80, 90, 100};
        int target = 70;

        int index = interpolationSearch(sortedArr, target);

        if (index != -1) {
            System.out.println("Element found at index: " + index);
        } else {
            System.out.println("Element not found.");
        }
    }
}

```

![[Pasted image 20250807100801.png]]


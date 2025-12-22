
#### BUBBLE SORT 
![[Pasted image 20250807142751.png]]

```java
import java.util.*;
public class Main
{
	public static void main(String[] args) {
	
	int arr[] = {7,9,5,10,14,15};
	int n = arr.length;
	for(int i=0;i<n-1;i++){
	    for(int j=0;j<n-i-1;j++){
	        if(arr[j] > arr[j+1]){
	            int temp = arr[j];
	            arr[j] = arr[j+1];
	            arr[j+1] = temp;
	        }
	    }
	}
	for(int i=0;i<n;i++){
	    System.out.println(arr[i]);
	}
	}
}

```

#### SELECTION SORT 

![[Pasted image 20250809132019.png]]

```java
public class SelectionSort {
    public static void selectionSort(int[] arr) {
        int n = arr.length;

        for (int i = 0; i < n - 1; i++) {
            // Find the index of minimum element
            int minIdx = i;
            for (int j = i + 1; j < n; j++)
                if (arr[j] < arr[minIdx])
                    minIdx = j;

            // Swap the found minimum with the first element
            int temp = arr[minIdx];
            arr[minIdx] = arr[i];
            arr[i] = temp;
        }
    }
}
```

#### INSERTION SORT 
![[Pasted image 20250809133310.png]]

```java
public class InsertionSort {
    public static void insertionSort(int[] arr) {
        int n = arr.length;

        for (int i = 1; i < n; i++) {
            int key = arr[i];
            int j = i - 1;

            // Move elements greater than key to one position ahead
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j = j - 1;
            }
            arr[j + 1] = key;
        }
    }
}
```

#### MERGE SORT 
![[Pasted image 20250809143140.png]]

```java
public class Main{
    public static void main(String args[])
    {   	
        int[] array = {8, 2, 5, 3, 4, 7, 6, 1};
        mergeSort(array);
        for(int i = 0; i < array.length; i++){
            System.out.print(array[i]+ " ");
        }
    }
	private static void mergeSort(int[] array) {
		int length = array.length;
		if (length <= 1) return; //base case
		
		int middle = length / 2;
		int[] leftArray = new int[middle];
		int[] rightArray = new int[length - middle];
		
		int i = 0; //left array
		int j = 0; //right array
		
		for(; i < length; i++) {
			if(i < middle) {
				leftArray[i] = array[i];
			}
			else {
				rightArray[j] = array[i];
				j++;
			}
		}
		mergeSort(leftArray);
		mergeSort(rightArray);
		merge(leftArray, rightArray, array);
	}
	
	private static void merge(int[] leftArray, int[] rightArray, int[] array) {
		
		int leftSize = array.length / 2;
		int rightSize = array.length - leftSize;
		int i = 0, l = 0, r = 0; //indices
		
		//check the conditions for merging
		while(l < leftSize && r < rightSize) {
			if(leftArray[l] < rightArray[r]) {
				array[i] = leftArray[l];
				i++;
				l++;
			}
			else {
				array[i] = rightArray[r];
				i++;
				r++;
			}
		}
		while(l < leftSize) {
			array[i] = leftArray[l];
			i++;
			l++;
		}
		while(r < rightSize) {
			array[i] = rightArray[r];
			i++;
			r++;
		}
	}
}
```

#### QUICK SORT 
![[Pasted image 20250810124920.png]]

```java
public class Main {
    public static void main(String args[]) {
        int[] array = {8, 2, 5, 3, 9, 4, 7, 6, 1};
        quickSort(array, 0, array.length - 1);
        for (int i : array) {
            System.out.print(i + " ");
        }
    }

    private static void quickSort(int[] array, int start, int end) {
        if (end <= start) return;
        int pivot = partition(array, start, end);
        quickSort(array, start, pivot - 1);
        quickSort(array, pivot + 1, end);
    }

    private static int partition(int[] array, int start, int end) {
        int pivot = array[end];
        int i = start - 1;
        for (int j = start; j <= end; j++) {
            if (array[j] < pivot) {
                i++;
                int temp = array[i];
                array[i] = array[j];
                array[j] = temp;
            }
        }
        i++;
        int temp = array[i];
        array[i] = array[end];
        array[end] = temp;
        return i;
    }
}

```
	- data elements are arranged **sequentially** or **linearly**
- each element is connected to its previous and next adjacent element.


 ### Characteristics:
- Elements are **stored in a linear order**.
- Every element has a **unique predecessor and successor** (except the first and last).
- Traversal is typically done in a **single run (start to end)**.

#### ARRAY
-  Stores elements in **contiguous memory**.
- Uses **indexing (0-based)** to access elements.
- Fixed size once declared.
- Arrays typically use **static memory allocation** / ****Contiguous Memory Allocation****
- ****Fixed Length:**** After creating an array, its size is fixed; we can not change it.
- ****Store Primitives and Objects****
![[Pasted image 20250805193346.png]]

```java
public class ArrayExample {
    public static void main(String[] args) {
        int[] arr = new int[5]; // Declare array of size 5
        arr[0] = 10;
        arr[1] = 20;
        arr[2] = 30;

        // Access and print elements
        for (int i = 0; i < arr.length; i++) {
            System.out.println("Element at index " + i + ": " + arr[i]);
        }
    }
}
```

#### STACK

- **LIFO**: Last In, First Out
- Push = insert, Pop = remove top element
- The Java Collection framework provides a Stack class
- ****empty, search, and peek, Push, Pop**** are the Methods in Stack 
```java
// Java code for stack implementation
import java.util.Stack;

class Example
{   
    // Pushing element on the top of the stack
    static void stack_push(Stack<Integer> stack)
    {
        for(int i = 0; i < 5; i++)
        {
            stack.push(i);
        }
    }
    
    // Popping element from the top of the stack
    static void stack_pop(Stack<Integer> stack)
    {
        System.out.println("Pop Operation:");

        for(int i = 0; i < 5; i++)
        {
            Integer y = (Integer) stack.pop();
            System.out.println(y);
        }
    }

    // Displaying element on the top of the stack
    static void stack_peek(Stack<Integer> stack)
    {
        Integer element = (Integer) stack.peek();
        System.out.println("Element on stack top: " + element);
    }
    
    // Searching element in the stack
    static void stack_search(Stack<Integer> stack, int element)
    {
        Integer pos = (Integer) stack.search(element);

        if(pos == -1)
            System.out.println("Element not found");
        else
            System.out.println("Element is found at position: " + pos);
    }


    public static void main (String[] args)
    {
        Stack<Integer> stack = new Stack<Integer>();

        stack_push(stack);
        stack_pop(stack);
        stack_push(stack);
        stack_peek(stack);
        stack_search(stack, 2);
        stack_search(stack, 6);
    }
}
```


#### QUEUE
- The ****Queue Interface**** is a part of java.util package and extends the Collection.
- Commonly used for task scheduling
- It supports iterating through elements
- follows the First-In, First-Out (FIFO) principle.
- **Enqueue:** Adding an element to the back (or tail) of the queue.
- **Dequeue:** Removing an element from the front (or head) of the queue.
- ****add(element)****: Adds an element to the rear of the queue. If the queue is full, it throws an exception.
  
##### Methods in Queue
- ****offer(element):**** Adds an element to the rear of the queue. If the queue is full, it returns false.
- ****remove()****: Removes and returns the element at the front of the queue. If the queue is empty, it throws an exception.
- ****poll():**** Removes and returns the element at the front of the queue. If the queue is empty, it returns null.
- ****element():**** Returns the element at the front of the queue without removing it. If the queue is empty, it throws an exception.
-  ****peek()****: Returns the element at the front of the queue without removing it. If the queue is empty, it returns null.

```java
import java.util.LinkedList;
import java.util.Queue;

public class sample {
    public static void main(String[] args) {
        Queue<String> queue = new LinkedList<>();

        // add elements to the queue
        queue.add("apple");
        queue.add("banana");
        queue.add("cherry");

        System.out.println("Queue: " + queue);

        // remove the element at the front of the queue
        String front = queue.remove();
        System.out.println("Removed element: " + front);

        // print the updated queue
        System.out.println("Queue after removal: " + queue);

        // add another element to the queue
        queue.add("date");

        // peek at the element at the front of the queue
        String peeked = queue.peek();
        System.out.println("Peeked element: " + peeked);

        // print the updated queue
        System.out.println("Queue after peek: " + queue);
    }
}
```

#### PRIORITY QUEUE 
-  part of the ****java.util**** package
- It implements a priority heap-based queue that processes elements based on their priority rather than the ****FIFO (First-In-First-Out)****
- based on the ****Priority Heap****.
- The size of the Priority Queue is dynamic
```java
// Java Program for PriorityQueue
import java.util.PriorityQueue;

public class Geeks 
{
    public static void main(String[] args) 
    {
      	// Priority Queue Min Type
        PriorityQueue<Integer> p = new PriorityQueue<>();

        // Add elements to the queue
        p.add(3);
        p.add(10);
        p.add(7);
        p.add(2);

        // Print the head of the queue
        System.out.println("Head of Queue: " + p.peek());//2

    }
}
```

#### LINKED LIST

- `LinkedList` is a class found in the `java.util`
- It is a fundamental data structure that implements the `List` and `Deque` (Double-Ended Queue) interfaces.
- the elements are not stored in contiguous locations
- each element is known as a node.
### Types of Linked Lists

1. **Singly Linked List** – each node points to the next one only
2. **Doubly Linked List** – each node points to both next and previous
3. **Circular Linked List** – last node points back to the first

![[Pasted image 20250806194210.png]]

![[Pasted image 20250806194254.png]]

- To make a linked list to work as a stack we use the methods push() and pop()
- To make a linked list to work as a queue we use the methods offer() and poll()


-  Linked list stores Nodes in 2 parts (data + address)
- Nodes are in non consecutive memory locations 
- Elements are linked using pointers 
![[Pasted image 20250806200750.png]]

```java
// Java Program to Demonstrate
// Implementation of LinkedList
// class
import java.util.*;

public class Geeks
{
    public static void main(String args[])
    {
        // Creating object of the
        // class linked list
        LinkedList<String> ll = new LinkedList<String>();

        // Adding elements to the linked list
        ll.add("A");
        ll.add("B");
        ll.addLast("C");
        ll.addFirst("D");
        ll.add(2, "E");

        System.out.println(ll);

        ll.remove("B");
        ll.remove(3);
        ll.removeFirst();
        ll.removeLast();

        System.out.println(ll);
    }
}
```

#### DYNAMIC ARRAY (ARRAY LIST)

- A **Dynamic Array** is an array that **automatically resizes** itself when more elements are added than its current capacity.
- Unlike a regular array (fixed size), dynamic arrays:
	- Allow **random access** (like arrays
	- **Resize themselves** when full
	- Combine **flexibility** and **speed**

- Java provides a **`java.util.ArrayList`** class which is a dynamic array implementation.

- A Graph is a non-linear data structure consisting of vertices and edges
-  The vertices are sometimes also referred to as nodes
-  edges are lines or arcs that connect any two nodes in the graph

Graphs are widely used in:
- Social networks (users as nodes, friendships as edges)
- Maps & navigation (locations as nodes, roads as edges)
- Recommendation systems
- Computer networks

## **Types of Graphs**
1. **Directed vs. Undirected**
    - Directed → Edges have direction (A → B)
    - Undirected → Edges are bidirectional (A ↔ B)
2. **Weighted vs. Unweighted**
    - Weighted → Each edge has a cost or weight.
    - Unweighted → All edges have equal cost.
3. **Cyclic vs. Acyclic**
    - Cyclic → Contains at least one cycle.
    - Acyclic → No cycles (e.g., Trees, DAGs).

![[Pasted image 20250810142535.png]]

![[Pasted image 20250810142551.png]]


## **Ways to Represent a Graph**

1. **Adjacency Matrix**
    - 2D array where `matrix[i][j]` stores the weight (or `1` if connected) between vertex `i` and `j`.
    - Easy to check if two vertices are connected (O(1)).
    - Uses **O(V²)** space.
![[Pasted image 20250810142751.png]]
- Adjacency Matrix = An array to store 1's/0's to represent edges
				       # of rows =    # of unique nodes
				       # of columns = # of unique nodes

```java
import java.util.ArrayList;
import java.util.*;
public class Main {
	public static void main(String[] args) {
		Graph graph = new Graph(5);
		
		graph.addNode(new Node('A'));
		graph.addNode(new Node('B'));
		graph.addNode(new Node('C'));
		graph.addNode(new Node('D'));
		graph.addNode(new Node('E'));
		
		graph.addEdge(0, 1);
		graph.addEdge(1, 2);
        graph.addEdge(1, 4); 
		graph.addEdge(2, 3);
		graph.addEdge(2, 4);
		graph.addEdge(4, 0);
		graph.addEdge(4, 2);
		
		graph.print();
		
		//System.out.println(graph.checkEdge(0, 1));
	}

public static class Graph {

	ArrayList<Node> nodes;
	
	int[][] matrix;
	
	Graph(int size){
		nodes = new ArrayList<>();
		matrix = new int[size][size];
	}
	
	public void addNode(Node node) {
		nodes.add(node);
	}
	
	public void addEdge(int src, int dst) {
		matrix[src][dst] = 1;
	}
	
	public boolean checkEdge(int src, int dst) {
		if(matrix[src][dst] == 1) {
			return true;
		}
		else {
			return false;
		}
	}
	
	public void print() {
		System.out.print("  ");
		for(Node node : nodes) {
			System.out.print(node.data + " ");
		}
		System.out.println();
		
		for(int i = 0; i < matrix.length; i++) {
			System.out.print(nodes.get(i).data + " ");
			for(int j = 0; j < matrix[i].length; j++) {
				System.out.print(matrix[i][j] + " ");
			}
			System.out.println();
		}
	}
}
public static class Node {

	char data;
	
	Node(char data){
		this.data = data;
	}
}
}
//output
  A B C D E 
A 0 1 0 0 0 
B 0 0 1 0 1 
C 0 0 0 1 1 
D 0 0 0 0 0 
E 1 0 1 0 0 

```




2. **Adjacency List**
    - An array/list where each element contains a list of connected vertices.
    - Saves space for sparse graphs.
    - Traversal is faster in sparse graphs.

![[Pasted image 20250810142815.png]]
- Adjacency List = An array/arraylist of linkedlists.
					          Each LinkedList has a unique node at the head.
					          All adjacent neighbors to that node are added to that node's linkedlist
		
						  runtime complexity to check an Edge: O(v)
						  space complexity: O(v + e)


```java
import java.util.*;
public class Main {

	public static void main(String[] args) {
		Graph graph = new Graph();
		
		graph.addNode(new Node('A'));
		graph.addNode(new Node('B'));
		graph.addNode(new Node('C'));
		graph.addNode(new Node('D'));
		graph.addNode(new Node('E'));
		
		graph.addEdge(0, 1);
		graph.addEdge(1, 2);
		graph.addEdge(1, 4);
		graph.addEdge(2, 3);
		graph.addEdge(2, 4);
		graph.addEdge(4, 0);
		graph.addEdge(4, 2);
		
		graph.print();
		
		//System.out.println(graph.checkEdge(0, 1));
	}
	
	public static class Graph {

	ArrayList<LinkedList<Node>> alist;
	
	Graph(){
		alist = new ArrayList<>();
	}
	
	public void addNode(Node node) {
		LinkedList<Node> currentList = new LinkedList<>();
		currentList.add(node);
		alist.add(currentList);
	}
	public void addEdge(int src, int dst) {
		LinkedList<Node> currentList = alist.get(src);
		Node dstNode = alist.get(dst).get(0);
		currentList.add(dstNode);
	}
	public boolean checkEdge(int src, int dst) {
		LinkedList<Node> currentList = alist.get(src);
		Node dstNode = alist.get(dst).get(0);
		
		for(Node node : currentList) {
			if(node == dstNode) {
				return true;
			}
		}
		return false;
	}
	public void print() {
		for(LinkedList<Node> currentList : alist) {
			for(Node node : currentList) {
				System.out.print(node.data + " -> ");
			}
			System.out.println();
		}
	}	
}
public static class Node {

	char data;
	
	Node(char data){
		this.data = data;
	}
}


}
//output
A -> B -> 
B -> C -> E -> 
C -> D -> E -> 
D -> 
E -> A -> C -> 

```


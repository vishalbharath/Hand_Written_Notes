- **Depth-First Search** is a graph traversal algorithm that starts from a given node (vertex) and explores as far as possible along each branch before backtracking.
- **Uses:** Path finding, cycle detection, topological sorting, solving puzzles like mazes.
- **Approaches:**
1. **Recursive DFS** (using the call stack)
2. **Iterative DFS** (using an explicit `Stack`)

## **Key Concepts**

- **Visited Array / Set** → Prevents revisiting the same node.
- **Adjacency List / Matrix** → Represents the graph.
- DFS can be applied to both **directed** and **undirected** graphs.

```java
import java.util.*;

public class DFSExample {
    private LinkedList<Integer>[] adj; // adjacency list
    private boolean[] visited;

    // Constructor
    DFSExample(int vertices) {
        adj = new LinkedList[vertices];
        visited = new boolean[vertices];
        for (int i = 0; i < vertices; i++) {
            adj[i] = new LinkedList<>();
        }
    }

    // Add edge
    void addEdge(int src, int dest) {
        adj[src].add(dest);
        adj[dest].add(src); // Remove this line for directed graph
    }

    // Recursive DFS
    void dfs(int vertex) {
        visited[vertex] = true;
        System.out.print(vertex + " ");

        for (int neighbor : adj[vertex]) {
            if (!visited[neighbor]) {
                dfs(neighbor);
            }
        }
    }

    public static void main(String[] args) {
        DFSExample graph = new DFSExample(6);

        // Adding edges
        graph.addEdge(0, 1);
        graph.addEdge(0, 2);
        graph.addEdge(1, 3);
        graph.addEdge(1, 4);
        graph.addEdge(2, 4);
        graph.addEdge(3, 5);
        graph.addEdge(4, 5);

        System.out.println("DFS Traversal starting from node 0:");
        graph.dfs(0);
    }
}
//output
DFS Traversal starting from node 0:
0 1 3 5 4 2

```


- #### **Iterative DFS (Using Stack)**
Sometimes recursion might cause a **stack overflow** for large graphs, so we use an explicit stack:
```java
void iterativeDFS(int start) {
    boolean[] visited = new boolean[adj.length];
    Stack<Integer> stack = new Stack<>();

    stack.push(start);

    while (!stack.isEmpty()) {
        int vertex = stack.pop();

        if (!visited[vertex]) {
            System.out.print(vertex + " ");
            visited[vertex] = true;

            // Push all unvisited neighbors
            for (int neighbor : adj[vertex]) {
                if (!visited[neighbor]) {
                    stack.push(neighbor);
                }
            }
        }
    }
}

```

## **Time & Space Complexity**

- **Time:** `O(V + E)`
    - `V` → Number of vertices
    - `E` → Number of edges
- **Space:** `O(V)` for visited array + recursion stack (or explicit stack)


![[Pasted image 20250813210137.png]]

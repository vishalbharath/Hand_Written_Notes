- Breadth-First Search is a graph traversal algorithm that explores **all nodes at the current depth before moving to the next depth**.
- It uses a **queue** to keep track of nodes to visit next.
- Works on **graphs** (directed or undirected) and **trees**.
- Uses **FIFO** (First In, First Out) ordering.
- Can find the **shortest path** in an unweighted graph.
- Avoids visiting nodes twice by using a **visited set** or array.


## **Algorithm Steps**

1. **Initialize**:
    - Create a queue and mark the start node as visited.
2. **Process**:
    - Dequeue a node.
    - Visit all its unvisited neighbors, mark them visited, and enqueue them.
3. **Repeat** until the queue is empty.

```java
import java.util.*;

public class BFSExample {
    // Function to perform BFS
    public static void bfs(Map<Integer, List<Integer>> graph, int start) {
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> visited = new HashSet<>();

        // Start BFS from the given start node
        queue.add(start);
        visited.add(start);

        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");

            // Visit all unvisited neighbors
            for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
                if (!visited.contains(neighbor)) {
                    queue.add(neighbor);
                    visited.add(neighbor);
                }
            }
        }
    }

    public static void main(String[] args) {
        // Representing the graph as an adjacency list
        Map<Integer, List<Integer>> graph = new HashMap<>();
        graph.put(0, Arrays.asList(1, 2));
        graph.put(1, Arrays.asList(0, 3, 4));
        graph.put(2, Arrays.asList(0, 5, 6));
        graph.put(3, Arrays.asList(1));
        graph.put(4, Arrays.asList(1));
        graph.put(5, Arrays.asList(2));
        graph.put(6, Arrays.asList(2));

        System.out.println("BFS Traversal starting from node 0:");
        bfs(graph, 0);
    }
}
//output
BFS Traversal starting from node 0:
0 1 2 3 4 5 6

```


## **Time & Space Complexity**

- **Time Complexity:** `O(V + E)`
    - `V` = number of vertices, `E` = number of edges.
- **Space Complexity:** `O(V)` for the queue and visited set.

![[Pasted image 20250813210114.png]]
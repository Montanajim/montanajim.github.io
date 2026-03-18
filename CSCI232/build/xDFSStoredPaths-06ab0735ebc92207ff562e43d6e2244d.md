

# DFS - Stored Paths



This Java code defines a `DFS` class that implements Depth-First Search for an undirected graph represented using an adjacency list. It provides standard DFS traversal methods (both recursive and iterative) that print the visited node order, as well as specialized methods (also recursive and iterative) designed to find and store all possible paths starting from a given source vertex discovered during the DFS exploration. The `Main` class demonstrates how to create a graph, add edges, and utilize both the traversal and path-finding functionalities provided by the `DFS` class.

Java

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.HashMap;
import java.util.LinkedList;
import java.util.List;
import java.util.Map;
import java.util.Stack;

class DFS {

    // Num Vertices
    private final int numVertices;

    // Adjacency list to store edges
    public final List<LinkedList<Integer>> adjencyList;

    // List to store all paths found by the last DFS run
    private List<List<Integer>> allPaths;

    // Constructor
    public DFS(int vertices) {
        this.numVertices = vertices;
        this.adjencyList = new ArrayList<>(vertices);
        this.allPaths = new ArrayList<>(); // Initialize the path list

        for (int i = 0; i < vertices; i++) {
            this.adjencyList.add(new LinkedList<>());
        }
    }

    // Add edges (undirected graph)
    public void addEdge(int source, int destination) {
        // Ensure vertices are within bounds
        if (source < 0 || source >= numVertices || destination < 0 || destination >= numVertices) {
            System.err.println("Warning: Vertex index out of bounds. Edge not added.");
            return;
        }
        adjencyList.get(source).add(destination);
        adjencyList.get(destination).add(source); // For undirected graph
    }

    // --- Recursive DFS Path Finding ---

    /**
     * Finds all paths starting from startVertex using recursive DFS.
     * Stores the paths in the allPaths list.
     *
     * @param startVertex The vertex to start the search from.
     */
    public void findAllPathsRecursive(int startVertex) {
        if (startVertex < 0 || startVertex >= numVertices) {
             System.err.println("Error: Start vertex out of bounds.");
             return;
        }
        boolean[] visited = new boolean[numVertices];
        this.allPaths = new ArrayList<>(); // Reset paths for new search
        List<Integer> currentPath = new ArrayList<>();

        System.out.println("\nFinding all paths (Recursive DFS) starting from vertex " + startVertex + ":");
        findAllPathsRecursiveUtil(startVertex, visited, currentPath);
    }

    /**
     * Recursive helper function for DFS path finding.
     *
     * @param vertex      The current vertex being visited.
     * @param visited     Array to keep track of visited nodes in the current recursion path.
     * @param currentPath The path taken to reach the current vertex.
     */
    private void findAllPathsRecursiveUtil(int vertex, boolean[] visited, List<Integer> currentPath) {
        // Mark the current node as visited and add it to the path
        visited[vertex] = true;
        currentPath.add(vertex);

        // Store a copy of the current path
        // This captures the path to the *current* vertex
        allPaths.add(new ArrayList<>(currentPath));
        // System.out.println("Path found: " + currentPath); // Optional: print paths as they are found

        // Recur for all adjacent vertices
        for (int neighbor : adjencyList.get(vertex)) {
            if (!visited[neighbor]) {
                findAllPathsRecursiveUtil(neighbor, visited, currentPath);
            }
        }

        // Backtrack: remove current vertex from path and mark as unvisited
        // for other potential paths.
        currentPath.remove(currentPath.size() - 1);
        visited[vertex] = false;
    }


    // --- Iterative DFS Path Finding ---

     /**
      * Finds paths using iterative DFS and stores them.
      * This version uses a stack storing pairs of (node, path_to_node).
      * Note: The order of path discovery might differ from the recursive version.
      *
      * @param startVertex The vertex to start the search from.
      */
    public void findAllPathsIterative(int startVertex) {
         if (startVertex < 0 || startVertex >= numVertices) {
             System.err.println("Error: Start vertex out of bounds.");
             return;
         }
         this.allPaths = new ArrayList<>(); // Reset paths
         System.out.println("\nFinding all paths (Iterative DFS) starting from vertex " + startVertex + ":");

         // Stack stores pairs: the node and the path to reach it
         Stack<Pair<Integer, List<Integer>>> stack = new Stack<>();

         // Initial path contains only the start vertex
         List<Integer> initialPath = new ArrayList<>();
         initialPath.add(startVertex);
         stack.push(new Pair<>(startVertex, initialPath));

         // Keep track of visited nodes *globally* across different path explorations
         // This prevents infinite loops in cyclic graphs and redundant processing.
         boolean[] globallyVisited = new boolean[numVertices];


         while (!stack.isEmpty()) {
             Pair<Integer, List<Integer>> currentPair = stack.pop();
             int currentVertex = currentPair.getKey();
             List<Integer> currentPath = currentPair.getValue();

             // If we haven't processed this node *through this specific path expansion*
             // Mark it visited *globally* only after processing its path.
             // This allows finding different paths to the same node, but standard
             // iterative DFS usually uses a simpler visited check.
             // For simplicity matching the recursive intent, let's only proceed
             // if the node hasn't been the *end* of a stored path yet.
             // A better approach might be needed for complex path requirements.

             // Store the path found to this vertex
             allPaths.add(new ArrayList<>(currentPath)); // Store a copy
             // System.out.println("Path found: " + currentPath); // Optional: print


             if (!globallyVisited[currentVertex]) {
                 globallyVisited[currentVertex] = true; // Mark globally visited

                  // Explore neighbors
                 // Iterate in reverse to mimic recursive DFS neighbor order more closely (optional)
                 List<Integer> neighbors = adjencyList.get(currentVertex);
                 // Collections.reverse(neighbors); // Uncomment to push neighbors in reverse order

                 for (int neighbor : neighbors) {
                     // Check if the neighbor is already in the *current* path to avoid cycles within a single path
                     boolean visitedInCurrentPath = false;
                     for(int nodeInPath : currentPath) {
                         if (nodeInPath == neighbor) {
                             visitedInCurrentPath = true;
                             break;
                         }
                     }

                     // If the neighbor hasn't been visited *in this specific path*
                     if (!visitedInCurrentPath) {
                         List<Integer> newPath = new ArrayList<>(currentPath);
                         newPath.add(neighbor);
                         stack.push(new Pair<>(neighbor, newPath));
                     }
                 }
                 // Collections.reverse(neighbors); // Reverse back if reversed earlier
             }
         }
     }


    // --- Original Traversal Methods (for comparison/demonstration) ---

    /**
     * Performs the original iterative DFS traversal, printing nodes as visited.
     * Does not store paths.
     * @param startVertex The vertex to start from.
     */
    public void performDFSTraversalIterative(int startVertex) {
        if (startVertex < 0 || startVertex >= numVertices) {
            System.err.println("Error: Start vertex out of bounds.");
            return;
        }
        boolean[] visited = new boolean[numVertices];
        Stack<Integer> stack = new Stack<>(); // Use Stack's push/pop for LIFO (DFS)

        visited[startVertex] = true;
        stack.push(startVertex); // Push onto stack

        System.out.println("\nDFS Traversal Order (Iterative): starting from " + startVertex + " ");

        while (!stack.isEmpty()) {
            int currentVertex = stack.pop(); // Pop from stack (LIFO)
            System.out.print(currentVertex + " ");

            // Get neighbors and push unvisited ones onto the stack
            // Process neighbors in natural order (or reverse to mimic recursion)
            List<Integer> neighbors = adjencyList.get(currentVertex);
             // Collections.reverse(neighbors); // To more closely match typical recursive order

            for (int neighbor : neighbors) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    stack.push(neighbor);
                }
            }
             // Collections.reverse(neighbors); // Reverse back if needed
        }
        System.out.println();
    }

     /**
     * Performs the original recursive DFS traversal, printing nodes as visited.
     * Does not store paths.
     * @param startVertex The vertex to start from.
     */
    public void performDFSTraversalRecursive(int startVertex) {
         if (startVertex < 0 || startVertex >= numVertices) {
             System.err.println("Error: Start vertex out of bounds.");
             return;
         }
        boolean[] visited = new boolean[numVertices];
        System.out.println("\nDFS Traversal Order (Recursive) starting from vertex " + startVertex + ":");
        performDFSTraversalRecursiveUtil(startVertex, visited);
        System.out.println();
    }

    private void performDFSTraversalRecursiveUtil(int vertex, boolean[] visited) {
        visited[vertex] = true;
        System.out.print(vertex + " ");

        for (int neighbor : adjencyList.get(vertex)) {
            if (!visited[neighbor]) {
                performDFSTraversalRecursiveUtil(neighbor, visited);
            }
        }
    }

    // --- Utility ---

    /**
     * Returns the list of paths found by the last pathfinding call.
     * @return A list where each element is a list of integers representing a path.
     */
    public List<List<Integer>> getAllPaths() {
        return allPaths;
    }

     /**
      * Prints all stored paths.
      */
     public void printAllPaths() {
         if (allPaths == null || allPaths.isEmpty()) {
             System.out.println("No paths have been generated or stored yet.");
             return;
         }
         System.out.println("\n--- Stored Paths ---");
         int pathNum = 1;
         for (List<Integer> path : allPaths) {
             System.out.println("Path " + (pathNum++) + ": " + path);
         }
         System.out.println("--------------------");
     }

     // Simple generic Pair class (or use javafx.util.Pair if available/allowed)
     private static class Pair<K, V> {
         private final K key;
         private final V value;

         public Pair(K key, V value) {
             this.key = key;
             this.value = value;
         }

         public K getKey() { return key; }
         public V getValue() { return value; }
     }
}

class Main {

    public static void main(String[] args) {

        DFS graph = new DFS(12);

        // Build the graph
        graph.addEdge(0, 1);
        graph.addEdge(0, 2);
        graph.addEdge(1, 3);
        graph.addEdge(2, 4);
        graph.addEdge(4, 5);
        graph.addEdge(0, 6); // 0 -> 6
        graph.addEdge(0, 7); // 0 -> 7
        graph.addEdge(7, 8); // 7 -> 8
        graph.addEdge(7, 9); // 7 -> 9
        graph.addEdge(9, 10); // 9 -> 10
        graph.addEdge(5, 11); // 5 -> 11

        // Print Adjacency List (for verification)
        System.out.println("--- Adjacency List ---");
        for (int i = 0; i < graph.adjencyList.size(); i++) {
            System.out.println("Vertex " + i + ": " + graph.adjencyList.get(i));
        }
         System.out.println("----------------------");

        // --- Demonstrate Original Traversals ---
        graph.performDFSTraversalIterative(0);
        graph.performDFSTraversalRecursive(0);

        // --- Find and Store Paths (Recursive) ---
        graph.findAllPathsRecursive(0);
        // Print the paths found by the recursive method
        graph.printAllPaths();

        // --- Find and Store Paths (Iterative) ---
        graph.findAllPathsIterative(0);
         // Print the paths found by the iterative method
         // Note: The order and exact paths might differ slightly depending on implementation details
         graph.printAllPaths();

         // Example: Get paths and process them
         System.out.println("\nAccessing paths manually after iterative search:");
         List<List<Integer>> storedPaths = graph.getAllPaths();
         if (storedPaths != null && !storedPaths.isEmpty()) {
             System.out.println("Total paths found: " + storedPaths.size());
             System.out.println("First path found: " + storedPaths.get(0));
             System.out.println("Last path found: " + storedPaths.get(storedPaths.size() - 1));
         }
    }
}
```



This code defines a `DFS` class that represents a graph and provides methods for performing Depth-First Search (DFS) operations on it. It specifically includes implementations for:

1. **Standard DFS Traversal (Recursive & Iterative):** These methods visit nodes in DFS order and typically print them, primarily demonstrating the traversal algorithm itself.
2. **Finding All Paths via DFS (Recursive & Iterative):** These are more complex methods designed to find and store *all* possible paths starting from a given vertex that can be discovered through a DFS exploration.

Here's a breakdown of the components:

**`DFS` Class:**

1. **Fields:**

   - `numVertices`: An integer storing the number of vertices in the graph.
   - `adjencyList`: A `List<LinkedList<Integer>>`. This is the core graph representation using an **adjacency list**. The outer list has an index for each vertex (0 to `numVertices - 1`). The `LinkedList` at each index `i` stores the vertices directly connected (adjacent) to vertex `i`.
   - `allPaths`: A `List<List<Integer>>`. This list is used to store the results of the path-finding operations (`findAllPathsRecursive` or `findAllPathsIterative`). Each element within `allPaths` is itself a `List<Integer>` representing a single path found.

2. **Constructor (`DFS(int vertices)`):**

   - Initializes the graph with a specified number of vertices.
   - Creates the `adjencyList` structure, adding an empty `LinkedList` for each vertex.
   - Initializes the `allPaths` list.

3. **`addEdge(int source, int destination)`:**

   - Adds an edge between the `source` vertex and the `destination` vertex.
   - Includes basic error checking to ensure vertex indices are valid.
   - Adds `destination` to `source`'s list and `source` to `destination`'s list. This makes the graph **undirected** (an edge exists in both directions).

4. **Recursive Path Finding (`findAllPathsRecursive` and `findAllPathsRecursiveUtil`):**

   - `findAllPathsRecursive(startVertex)`: The public method to initiate the search. It sets up a `visited` array (local to the current path exploration) and resets the `allPaths` list before calling the helper function.

   - ```
     findAllPathsRecursiveUtil(vertex, visited, currentPath)
     ```

     :

     - This is the core recursive logic.
     - It marks the current `vertex` as visited *for the current path exploration*.
     - Adds the `vertex` to the `currentPath`.
     - **Crucially:** It adds a *copy* of the `currentPath` (up to the current `vertex`) to the `allPaths` list. This means every node encountered during the DFS becomes the end of a stored path.
     - It iterates through the neighbors of the current `vertex`. If a neighbor hasn't been visited *in the current recursive call stack*, it recursively calls itself for that neighbor.
     - **Backtracking:** After exploring all paths stemming from the current `vertex`, it removes the `vertex` from `currentPath` and marks it as unvisited (`visited[vertex] = false`). This is essential to allow the algorithm to explore *other* paths that might reach this `vertex` through a different sequence.

5. **Iterative Path Finding (`findAllPathsIterative`):**

   - This method attempts to find all paths using an iterative approach with a `Stack`.

   - It uses a 

     ```
     Stack
     ```

      where each element is a 

     ```
     Pair
     ```

      containing:

     - The current vertex (`Integer`).
     - The path (`List<Integer>`) taken to reach that vertex.

   - It also uses a 

     ```
     globallyVisited
     ```

      array. The logic here is slightly different from the recursive version's 

     ```
     visited
     ```

      array:

     - It adds the path to `allPaths` *when* a `Pair` is popped from the stack.
     - It checks `globallyVisited` *after* storing the path. If the node hasn't been globally visited yet, it marks it and explores its neighbors.
     - When exploring neighbors, it checks if the neighbor is already present in the *current specific path* (`visitedInCurrentPath` loop) to prevent cycles *within that single path*.
     - If a neighbor is valid (not creating a cycle in the current path), a new path is created by extending the current one, and a new `Pair` is pushed onto the stack.

   - **Note:** The use of `globallyVisited` prevents re-exploring *from* a node once *any* path ending there has been processed. This helps avoid infinite loops in cyclic graphs but might prune some paths compared to a pure recursive backtracking approach if the goal was *all simple paths*. The order of paths found might also differ from the recursive version due to stack LIFO order and neighbor processing order.

6. **Standard Traversal Methods (`performDFSTraversalIterative`, `performDFSTraversalRecursive`, `performDFSTraversalRecursiveUtil`):**

   - These implement the more "standard" DFS algorithm where the goal is just to visit each reachable node once.
   - They use a `visited` array to keep track of nodes already visited during the *entire* traversal.
   - They print the vertex when it's visited (recursive) or popped (iterative).
   - They do **not** store paths.

7. **Utility Methods:**

   - `getAllPaths()`: Returns the `allPaths` list (containing results from the last path-finding call).
   - `printAllPaths()`: Prints all the paths currently stored in the `allPaths` list in a readable format.
   - `Pair<K, V>`: A simple private static inner class to hold pairs of objects (used in the iterative path finding).

**`Main` Class:**

- Creates an instance of the `DFS` graph with 12 vertices.
- Adds edges to define the graph structure.
- Prints the adjacency list to show the graph's structure.
- Demonstrates the standard iterative and recursive DFS *traversals*, printing the order nodes are visited.
- Calls `findAllPathsRecursive(0)` to find paths starting from vertex 0 using recursion and prints the results.
- Calls `findAllPathsIterative(0)` to find paths starting from vertex 0 using iteration and prints those results.
- Shows how to retrieve the list of paths using `getAllPaths()` after a search.

In essence, this code provides a robust `DFS` class for undirected graphs, offering both standard traversal and more complex path-finding capabilities, implemented recursively and iteratively.
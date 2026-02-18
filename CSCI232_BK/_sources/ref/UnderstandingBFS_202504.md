# Understanding Breadth-First Search (BFS)


## What is BFS?

Imagine you're exploring a maze. BFS is like exploring it level by level. You start at the entrance (the *source node*). First, you check all the paths directly connected to the entrance (one step away). Then, you explore all the paths that are two steps away from the entrance, then three steps away, and so on. You explore *broadly* before going *deeper* into any one path.

In technical terms, BFS is an algorithm for traversing or searching tree or graph data structures. It starts at a selected node (the source) and explores all of the neighbor nodes at the present depth or level  prior to moving on to the nodes at the next depth level. It uses a queue (First-In, First-Out) data structure to keep track of the next node to visit.

## Why Use BFS?

BFS is particularly useful for a few key tasks:

1. **Finding the Shortest Path:** In graphs where all edges have the same "cost" or weight (like in the maze example, where each step is equal), BFS is guaranteed to find the shortest path between the starting node and any other reachable node in terms of the number of edges.
2. **Level Order Traversal:** It naturally visits nodes level by level, which can be useful in hierarchical structures.
3. **Connectivity Checking:** You can use BFS to determine if a node is reachable from a starting node or to find all reachable nodes.

### Real-Life Examples

BFS is used in many applications:

1. **Social Networks:** Finding friends-of-friends. If you want to see all people within 'X' connections of you, BFS is a natural fit. It explores your direct friends (level 1), then their friends (level 2), and so on.
2. **GPS Navigation:** Finding the shortest route (in terms of number of turns or segments, not necessarily distance/time if roads have different speeds/lengths) between two points on a map.
3. **Web Crawlers:** Search engines use crawlers to discover web pages. A crawler might start at a seed page and use BFS to find all pages linked from it (level 1), then all pages linked from those pages (level 2), etc.
4. **Network Broadcasting:** Sending a message to all nodes in a network efficiently.
5. **Finding Connected Components:** Identifying groups of interconnected nodes in a graph.
---
<p style="page-break-after: always;">&nbsp;</p>
## Code Example

### Code Analysis
1. **`BFS`** Class: This class represents the graph itself.
   - `numVertices`: Stores the total number of nodes (vertices) in the graph.
   - `adjacencyList`: This is the core data structure for storing the graph. It's a `List` where each index corresponds to a vertex. The element at each index is a `LinkedList<Integer>` containing all the vertices directly connected to that vertex (its neighbors). This is called an *adjacency list representation*.
   - `BFS(int vertices)` (Constructor): Initializes the graph with a specific number of vertices and creates empty adjacency lists for each.
   - `addEdge(int source, int destination)`: Adds a connection (an edge) between two vertices. Since it adds the destination to the source's list *and* the source to the destination's list, it creates an *undirected* edge (meaning the connection goes both ways).
2. **`performBFS(int startVertex)`** Method: This is where the BFS magic happens.
   - `visited`: A boolean array to keep track of which vertices have already been visited. This prevents infinite loops in graphs with cycles.
   - `queue`: A `Queue` (implemented using `LinkedList`) is used to store the vertices to be visited. BFS relies on the FIFO (First-In, First-Out) nature of a queue.
   - **Initialization:** The `startVertex` is marked as visited and added to the queue.
   - **`Traversal Loop (while (!queue.isEmpty()))`**: The loop continues as long as there are nodes in the queue waiting to be processed.
     - `currentVertex = queue.poll()`: Removes the next vertex from the front of the queue. This is the vertex currently being visited.
     - `System.out.print(currentVertex + " ");`: Prints the visited vertex.
     - **`Neighbor Exploration (for (int neighbor : ...)):`** It iterates through all the neighbors of the `currentVertex` (obtained from the `adjacencyList`).
     - `if (!visited[neighbor])`: Checks if the neighbor has already been visited.
     - **Enqueueing:** If the neighbor hasn't been visited, it's marked as `visited` and added to the *end* of the queue (`queue.offer(neighbor)`). This ensures that nodes at the current level are fully explored before moving to the next level.
3. **`BreadthFirst_Rev2504`** Class (Main Program):
   - `main(String[] args)`: The entry point of the program.
   - Creates a `BFS` graph object with 11 vertices.
   - Calls `addEdge` multiple times to define the connections in the graph, matching the diagram in the comments.
   - Calls `performBFS(0)` to run BFS starting from vertex 0.
   - Calls `performBFS(6)` to run BFS starting from vertex 6, demonstrating how the traversal changes based on the starting point.

In essence, the code sets up a graph using adjacency lists and then implements the BFS algorithm using a queue and a visited array to explore the graph level by level, printing the nodes in the order they are visited.

<p style="page-break-after: always;">&nbsp;</p>
```java
/*
BREADTH FIRST
Developer: James Goudy
 */
package breadthfirst_rev2504a;

import java.util.LinkedList;
import java.util.Queue;
import java.util.List;
import java.util.ArrayList;


// Class representing a graph using adjacency lists
class BFS {

    // Total number of vertices in the graph
    private int numVertices;

    // Adjacency list to store edges
    private List<LinkedList<Integer>> adjacencyList;

    // Constructor to initialize the graph
    public BFS(int vertices) {
        this.numVertices = vertices;
        this.adjacencyList = new ArrayList<>(vertices);

        // Initialize each adjacency list for every vertex
        for (int i = 0; i < vertices; i++) {
            this.adjacencyList.add(new LinkedList<>());
        }
    }

    // Method to add an edge between two vertices
    public void addEdge(int source, int destination) {

        this.adjacencyList.get(source).add(destination);

        // For an undirected graph
        this.adjacencyList.get(destination).add(source);
    }

    // Method to perform Breadth-First Search starting from a given vertex (Iterative)
    public void performBFS(int startVertex) {

        // Track visited vertices
        boolean[] visited = new boolean[numVertices];

        // Queue to maintain BFS traversal order
        Queue<Integer> queue = new LinkedList<>();

        // Mark start vertex as visited
        visited[startVertex] = true;

        // Add start vertex to the queue
        queue.offer(startVertex);

        System.out.println("Breadth-First Search (Iterative) starting from vertex "
                                            + startVertex + ":");

        // Continue BFS traversal until queue becomes empty
        while (!queue.isEmpty()) {

            // Dequeue vertex from the queue
            int currentVertex = queue.poll();

            // Print the current vertex
            System.out.print(currentVertex + " ");

            // Explore all adjacent vertices of the current vertex
            for (int neighbor : this.adjacencyList.get(currentVertex)) {

                // If neighbor is not visited yet
                if (!visited[neighbor]) {

                    // Mark neighbor as visited
                    visited[neighbor] = true;

                    // Add neighbor to the queue
                    queue.offer(neighbor);
                }
            }
        }

        // Print newline after traversal completion
        System.out.println();
    }

    // Method to perform Breadth-First Search starting from a given vertex (Recursive)
    public void performBFSRecursive(int startVertex) {
        boolean[] visited = new boolean[numVertices];
        Queue<Integer> queue = new LinkedList<>();

        System.out.println("Breadth-First Search (Recursive) starting from vertex "
                                            + startVertex + ":");

        visited[startVertex] = true;
        queue.offer(startVertex);
        recursiveBFS(queue, visited);
        System.out.println();
    }

    private void recursiveBFS(Queue<Integer> queue, boolean[] visited) {
        if (queue.isEmpty()) {
            return;
        }

        int currentVertex = queue.poll();
        System.out.print(currentVertex + " ");

        for (int neighbor : this.adjacencyList.get(currentVertex)) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                queue.offer(neighbor);
            }
        }
        recursiveBFS(queue, visited);
    }
}

public class BreadthFirst_Rev2504a {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args)
    {
        BFS graph = new BFS(11);

        graph.addEdge(0, 1);
        graph.addEdge(0, 2);
        graph.addEdge(1, 3);
        graph.addEdge(2, 4);
        graph.addEdge(4, 5);

        graph.addEdge(0, 6);
        graph.addEdge(0, 7);
        graph.addEdge(7, 8);
        graph.addEdge(7, 9);

        graph.addEdge(9, 10);

        graph.performBFS(0);
        graph.performBFSRecursive(0);

        graph.performBFS(6);
        graph.performBFSRecursive(6);
    }

}

/*
 * Graph Map based on the addEdge calls:

       0
   /  /|\
  /  / | \
  1  2  6  7
  |  |    / \
  3  4   8   9
 |       |
  5        10

Breadth-First Search (Iterative) starting from vertex 0:
0 1 2 6 7 3 4 8 9 5 10 
Breadth-First Search (Recursive) starting from vertex 0:
0 1 2 6 7 3 4 8 9 5 10 
Breadth-First Search (Iterative) starting from vertex 6:
6 0 1 2 7 3 4 8 9 5 10 
Breadth-First Search (Recursive) starting from vertex 6:
6 0 1 2 7 3 4 8 9 5 10 

*/
```


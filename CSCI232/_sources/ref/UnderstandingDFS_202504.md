## Understanding Depth-First Search (DFS)

**What is DFS?**

Imagine exploring the same maze as before, but this time, instead of checking all paths at the current level, you pick one path and go as deep as possible until you hit a dead end. Then, you backtrack to the last branching point and try another path from there. You prioritize going deep down a single branch before exploring other branches.

In technical terms, DFS is an algorithm for traversing or searching tree or graph data structures. It starts at a selected node (the source) and explores as far as possible along each branch before backtracking. It uses a stack (Last-In, First-Out) data structure or recursion to keep track of the next node to visit.

**Why Use DFS?**

DFS is particularly useful for several key tasks:

- **Path Finding:** DFS can be used to find if a path exists between two nodes. It explores each path until it finds the target or exhausts all possibilities.
- **Detecting Cycles:** DFS can detect cycles in a graph. If you encounter a visited node that is still in the current recursion stack, it indicates a cycle.
- **Topological Sorting:** For directed acyclic graphs (DAGs), DFS can be used to perform a topological sort, which orders the nodes such that for every directed edge from node A to node B, node A comes before node B in the ordering.
- **Finding Connected Components:** Similar to BFS, DFS can be used to find all reachable nodes from a starting node and identify connected components in a graph.
- **Solving Puzzles:** Many puzzles that involve exploring possibilities, like Sudoku solvers or finding a path through a maze, can be effectively solved using DFS.

**Real-Life Examples**

DFS is used in various applications:

- **Backtracking Algorithms:** Many algorithms that involve trying out different possibilities and undoing choices if they don't lead to a solution use DFS principles.
- **Compiler Design:** DFS can be used in compilers for tasks like syntax analysis and semantic analysis.
- **File System Traversal:** When you explore folders and subfolders on your computer, many operating systems use a form of DFS.
- **Network Analysis:** Identifying dependencies or hierarchical structures in a network.

<p style="page-break-after: always;">&nbsp;</p>



**Code Example**



```
/*
DEPTH FIRST
Developer: James Goudy (Modified)
 */
package depthfirst_rev2504;

import java.util.LinkedList;
import java.util.List;
import java.util.ArrayList;
import java.util.Stack;

// Class representing a graph using adjacency lists
class DFS {

    // Total number of vertices in the graph
    private int numVertices;

    // Adjacency list to store edges
    private List<LinkedList<Integer>> adjacencyList;

    // Constructor to initialize the graph
    public DFS(int vertices) {
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

    // Method to perform Depth-First Search starting from a given vertex (Iterative)
    public void performDFSIterative(int startVertex) {
        boolean[] visited = new boolean[numVertices];
        Stack<Integer> stack = new Stack<>();

        visited[startVertex] = true;
        stack.push(startVertex);

        System.out.println("Depth-First Search (Iterative) starting from vertex "
                + startVertex + ":");

        while (!stack.isEmpty()) {
            int currentVertex = stack.pop();
            System.out.print(currentVertex + " ");

            for (int neighbor : this.adjacencyList.get(currentVertex)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    stack.push(neighbor);
                }
            }
        }
        System.out.println();
    }

    // Method to perform Depth-First Search starting from a given vertex (Recursive)
    public void performDFSRecursive(int startVertex) {
        boolean[] visited = new boolean[numVertices];
        System.out.println("Depth-First Search (Recursive) starting from vertex "
                + startVertex + ":");
        performDFSRecursiveUtil(startVertex, visited);
        System.out.println();
    }

    private void performDFSRecursiveUtil(int vertex, boolean[] visited) {
        visited[vertex] = true;
        System.out.print(vertex + " ");

        for (int neighbor : this.adjacencyList.get(vertex)) {
            if (!visited[neighbor]) {
                performDFSRecursiveUtil(neighbor, visited);
            }
        }
    }
}

public class DepthFirst_Rev2504 {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        DFS graph = new DFS(11);

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

        graph.performDFSIterative(0);
        graph.performDFSRecursive(0);

        graph.performDFSIterative(6);
        graph.performDFSRecursive(6);
    }

}

/*
 * Graph Map based on the addEdge calls:
 *
         0
       /  /|\
      /  / | \
     1  2  6  7
     |  |     / \
     3  4    8   9
        |        |
        5        10

Depth-First Search (Iterative) starting from vertex 0:
0 7 9 10 8 6 2 4 5 1 3
Depth-First Search (Recursive) starting from vertex 0:
0 1 3 2 4 5 7 8 9 10 6
Depth-First Search (Iterative) starting from vertex 6:
6 0 7 9 10 8 2 4 5 1 3
Depth-First Search (Recursive) starting from vertex 6:
6 0 1 3 2 4 5 7 8 9 10
*/
```

**Code Analysis**

**DFS Class:** This class represents the graph itself, similar to the BFS class.

- **`numVertices`:** Stores the total number of vertices in the graph.

- **`adjacencyList`:** The adjacency list representation of the graph.

- **`DFS(int vertices)` (Constructor):** Initializes the graph with a specified number of vertices and creates empty adjacency lists.

- **`addEdge(int source, int destination)`:** Adds an undirected edge between two vertices.

- `performDFSIterative(int startVertex)` Method:

   This method implements the iterative DFS algorithm.

  - **`visited`:** A boolean array to keep track of visited vertices.
  - **`stack`:** A `Stack` (LIFO - Last-In, First-Out) is used to store vertices to be visited. DFS relies on the LIFO nature of a stack to explore deeper first.
  - **Initialization:** The `startVertex` is marked as visited and pushed onto the stack.
  - **Traversal Loop (`while (!stack.isEmpty())`):** The loop continues as long as there are nodes in the stack to process.
  - **`currentVertex = stack.pop()`:** Removes the top vertex from the stack. This is the vertex currently being visited.
  - **`System.out.print(currentVertex + " ");`:** Prints the visited vertex.
  - **Neighbor Exploration (`for (int neighbor : ...)`):** It iterates through all the neighbors of the `currentVertex`.
  - **`if (!visited[neighbor])`:** Checks if the neighbor has already been visited.
  - **Pushing to Stack:** If the neighbor hasn't been visited, it's marked as visited and pushed onto the stack. This ensures that the algorithm explores the neighbors of the most recently added node first, going deeper into the graph.

- `performDFSRecursive(int startVertex)` Method:

   This method initiates the recursive DFS.

  - It creates a `visited` array and calls the helper method `performDFSRecursiveUtil`.

- `performDFSRecursiveUtil(int vertex, boolean[] visited)` Method:

   This is the recursive helper function.

  - It marks the current `vertex` as visited and prints it.
  - It then iterates through the neighbors of the current `vertex`.
  - For each unvisited neighbor, it recursively calls `performDFSRecursiveUtil` on that neighbor, effectively exploring deeper down that path.

**DepthFirst_Rev2504 Class (Main Program):**

- **`main(String[] args)`:** The entry point of the program.
- Creates a `DFS` graph object with 11 vertices.
- Calls `addEdge` multiple times to define the same graph connections as in the BFS example.
- Calls `performDFSIterative(0)` and `performDFSRecursive(0)` to run both iterative and recursive DFS starting from vertex 0.
- Calls `performDFSIterative(6)` and `performDFSRecursive(6)` to run both iterative and recursive DFS starting from vertex 6.

**Output**

The output shows the order in which the nodes are visited using both the iterative and recursive approaches of DFS, starting from different vertices. Notice how the traversal goes deep along one path before backtracking and exploring other paths, which is characteristic of Depth-First Search. The iterative and recursive approaches may result in slightly different traversal orders depending on the order in which neighbors are added to the stack or processed in the adjacency list.
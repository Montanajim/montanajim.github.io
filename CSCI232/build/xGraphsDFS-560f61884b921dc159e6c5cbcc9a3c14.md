# Depth-First Search (DFS)

Depth-First Search (DFS) is an algorithm for exploring tree or graph data structures. Imagine you're navigating a maze, and DFS is like taking a very narrow path, going as far as you can down one tunnel before checking any side passages. Here's how it works on graphs:

1. **Start at a Node:** You begin at any node (like the entrance to the maze).
1. **Explore Deepest Path:** Visit all the unvisited neighbors of that node (like going down the main tunnel).
1. **Mark and Backtrack:**  Mark the current node as visited to avoid revisiting it. If you reach a dead end (a node with no unvisited neighbors), backtrack to the most recent un-explored path (like going back to a fork in the maze and taking a different tunnel).
1. **Repeat:**  Keep repeating steps 2 and 3 until you've explored all possible paths from the starting node.

**Data Structures Used:**

- **Stack:** DFS typically uses a stack (LIFO - Last In, First Out) to keep track of the path being explored. Nodes are added to the stack as you move deeper into the graph, and removed as you backtrack.
- **Visited List:**  An additional data structure, like a visited list or array, is used to keep track of the nodes already explored and avoid revisiting them.

**Applications of DFS:**

- Finding paths in mazes or games.
- Topological sorting (ordering a directed acyclic graph where each node has dependencies only on nodes preceding it in the order).
- Cycle detection in graphs.
- Finding connected components in graphs (groups of nodes connected by edges).

**Advantages and Disadvantages:**

- **Advantages:** DFS can be efficient for certain graph structures and finding specific paths quickly.
- **Disadvantages:**  DFS might not be ideal for finding the shortest path between two nodes, and it can get stuck in infinite loops if there are cycles in the graph (without proper handling).

**Here are some resources for further learning:**

- A visual explanation of DFS on graphs: YouTube video on Depth First Search: [YouTube](https://gemini.google.com/app/371acaa163b28c36)
- A step-by-step explanation of the DFS algorithm: https://www.programiz.com/dsa/graph-dfs



## Lecture Code

```java
import java.util.ArrayList;
import java.util.List;

class Node {
  int data;
  boolean visited;

  public Node(int data) {
    this.data = data;
  }
}

class Graph {
  List<List<Node>> adjList;

  public Graph(int vertices) {
    adjList = new ArrayList<>(vertices);
    for (int i = 0; i < vertices; i++) {
      adjList.add(new ArrayList<>());
    }
  }

  public void addEdge(int src, int dest) {
    adjList.get(src).add(new Node(dest));
  }

  public void DFS(int startNode) {
    boolean visited[] = new boolean[adjList.size()];
    DFSUtil(startNode, visited);
  }

  private void DFSUtil(int node, boolean[] visited) {
    visited[node] = true;
    System.out.print(node + " ");

    // Visit all unvisited neighbors
    for (Node neighbor : adjList.get(node)) {
      if (!visited[neighbor.data]) {
        DFSUtil(neighbor.data, visited);
      }
    }
  }
}

public class Main {
  public static void main(String[] args) {
    int vertices = 6;
    Graph graph = new Graph(vertices);

    graph.addEdge(0, 1);
    graph.addEdge(0, 2);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(2, 3);
    graph.addEdge(4, 5);

    System.out.println("Depth First Traversal (starting from vertex 0)");
    
    for(int i= 0; i < vertices; i++)
    {
        System.out.print("V = " + i + " : ");
        graph.DFS(i);
        System.out.println();
    }
  }
}
/*
Depth First Traversal (starting from vertex 0)
V = 0 : 0 1 2 3 
V = 1 : 1 2 3 
V = 2 : 2 3 
V = 3 : 3 
V = 4 : 4 5 
V = 5 : 5 
*/
```




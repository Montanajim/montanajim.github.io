

# Breadth First

Breadth-First Search (BFS) is an algorithm used to traverse or search tree or graph data structures. It visits nodes level by level, exploring all the neighbor nodes at the current depth before moving down to the next level. Imagine exploring a maze - BFS would check every path on one floor before moving down to the floor below.

Here's a breakdown of BFS for graphs:

**Concept:**

1. Start at a chosen node (usually called the root node).
1. Visit all the unvisited neighbor nodes of the current node. Add them to a queue data structure (think of a line where you add people at the back).
1. Mark the current node as visited to avoid revisiting.
1. Dequeue a node from the queue (remove the first person in line). This becomes the current node.
1. Repeat steps 2-4 until the queue is empty.

**Key Points:**

- BFS uses a Queue to store neighbor nodes for exploration.  A Queue functions like "first in, first out"  - similar to a waiting line.
- It ensures we explore all nodes at a level before moving deeper into the graph.
- BFS is useful for finding shortest paths (assuming all edges have the same weight) in unweighted graphs.

**Example:**

Imagine a social network graph where nodes are people and edges are friendships. You can use BFS to find all your friends' friends (people two connections away). You'd start with yourself, then explore all your friends (level 1), then all their friends you haven't met yet (level 2).

**Further Exploration:**

- You can find visualizations of BFS on YouTube ([YouTube video on BFS]).
- For code examples, explore resources like GeeksforGeeks ([Breadth First Search for Graphs])



## Lecture Code

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;

public class BreadthFirstSearch {

  static class Graph {
    private int V; // number of vertices
    private List<List<Integer>> adj; // Adjacency List representation

    Graph(int V) {
      this.V = V;
      adj = new ArrayList<>(V);
      for (int i = 0; i < V; i++) {
        adj.add(new LinkedList<>());
      }
    }

    public void addEdge(int v, int w) {
      adj.get(v).add(w);
    }

    public void BFS(int s) {
      boolean visited[] = new boolean[V];

      LinkedList<Integer> queue = new LinkedList<Integer>();

      visited[s] = true;
      queue.add(s);

      while (queue.size() != 0) {
        s = queue.poll();
        System.out.print(s + " ");

        for (int neighbor : adj.get(s)) {
          if (!visited[neighbor]) {
            visited[neighbor] = true;
            queue.add(neighbor);
          }
        }
      }
    }
  }

  public static void main(String args[]) {

    int vertices = 4;

    BreadthFirstSearch.Graph g = new BreadthFirstSearch.Graph (vertices);


    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    System.out.println("Following is Breadth First Traversal (starting from vertex 0)");

    for(int i= 0; i < vertices; i++)
    {
        System.out.print("V = " + i + " : ");
        g.BFS(i);
        System.out.println();
    }
  }
}
/*
Following is Breadth First Traversal (starting from vertex 0)
V = 0 : 0 1 2 3 
V = 1 : 1 2 0 3 
V = 2 : 2 0 3 1 
V = 3 : 3 
*/
```

This code defines a `Graph` class with an adjacency list to represent the graph. The `BFS` method takes a starting vertex `s` and performs the following steps:

1. Creates a boolean array `visited` to keep track of visited nodes.
2. Initializes a queue using `LinkedList` to store nodes for exploration.
3. Marks the starting node `s` as visited and adds it to the queue.
4. Loops as long as the queue is not empty:
    * Dequeues a node from the queue (the current node).
    * Prints the current node.
    * Iterates through the neighbors of the current node.
      * If a neighbor is not visited, mark it visited and add it to the queue.

This ensures a level-by-level exploration of the graph.  
# Dijkstra’s Algorithm

## Shortest Paths in Weighted Graphs

## Introduction

You are handed a network—roads, routers, dependencies—each connection carrying a cost. The question is simple and ruthless: what is the cheapest path from one point to every other?

Brute force explores everything and collapses under scale. Dijkstra’s Algorithm refuses that chaos. It commits early, chooses wisely, and never looks back.

This chapter builds the algorithm from its core invariant—**relaxation**—and drives it into a clean, correct Java implementation.

------

## Chapter at a Glance

Dijkstra’s Algorithm computes shortest paths from a single source in a weighted graph with non-negative edges. It iteratively selects the closest unvisited vertex and improves paths through it using **relaxation**.

------

## Learning Goals

By the end of this chapter, you should be able to:

- Define relaxation precisely and apply it correctly
- Implement Dijkstra’s Algorithm in Java
- Trace execution and verify correctness
- Identify invalid use cases (negative weights)
- Compare Dijkstra’s Algorithm with alternative approaches

------

## What This Concept Is

Dijkstra’s Algorithm is a **greedy algorithm** that builds shortest paths incrementally.

### Definition

A **shortest path** is a path between two vertices such that the sum of edge weights is minimized.

### Definition (Relaxation)

**Relaxation** is the process of checking whether a shorter path to a vertex can be found through another vertex and updating the distance if so.

Formally:

If
`dist[u] + weight(u, v) < dist[v]`
then update
`dist[v] = dist[u] + weight(u, v)`

### Key Point

Relaxation is the beating heart of Dijkstra’s Algorithm. Every edge is a candidate for improvement. Most fail. The ones that succeed reshape the solution.

------

## Why This Concept Matters

Shortest path computation is foundational:

- Network routing (OSPF, BGP optimizations)
- Navigation systems
- Dependency resolution in compilers and build systems
- AI pathfinding in games

### Industry Relevance

Routing protocols such as OSPF implement variants of Dijkstra’s Algorithm to compute optimal paths across large, dynamic networks.

------

## Syntax and Basic Form (Java)

You need:

- An adjacency list representation
- A distance array
- A priority queue (min-heap)

### Core Structures

```java
import java.util.*;

// Represents a directed edge with a destination and weight
class Edge {
    int target;
    int weight;

    public Edge(int target, int weight) {
        this.target = target;
        this.weight = weight;
    }
}
```

------

## Core Behavior

Execution unfolds in a disciplined loop:

1. Initialize all distances to infinity
2. Set source distance to 0
3. Use a priority queue to select the closest vertex
4. Relax all outgoing edges
5. Mark vertex as finalized
6. Repeat

### Key Point

Once a vertex is finalized (visited), its shortest distance is guaranteed.

------

## Simple Example

Graph:

```
A --(4)--> B
A --(2)--> C
C --(1)--> B
B --(5)--> D
C --(8)--> D
```

From A:

- C becomes 2
- B improves from 4 to 3 via C
- D becomes 8

Notice the moment of truth: **relaxation** replaces a worse path (A→B = 4) with a better one (A→C→B = 3).

------

## Detailed Walkthrough (Java Implementation)

```java

package dijkstraexample;

// Represents a directed edge with a destination and weight

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;
import java.util.PriorityQueue;

class Edge {

    int target;
    int weight;

    public Edge(int target, int weight) {
        this.target = target;
        this.weight = weight;
    }
}

public class DijkstraExample {

// Dijkstra's algorithm implementation
    public static void dijkstra(List<List<Edge>> graph, int source) {
        int n = graph.size();

        // Distance array initialized to "infinity"
        int[] dist = new int[n];
        Arrays.fill(dist, Integer.MAX_VALUE);

        // Distance to source is 0
        dist[source] = 0;

        // Priority queue ordered by smallest distance
        PriorityQueue<Integer> pq = new PriorityQueue<>(Comparator.comparingInt(v -> dist[v]));
        pq.add(source);

        // Track finalized (visited) vertices
        boolean[] visited = new boolean[n];

        while (!pq.isEmpty()) {
            int current = pq.poll();

            // Skip if already processed
            if (visited[current]) {
                continue;
            }
            visited[current] = true;

            // Traverse neighbors of current vertex
            for (Edge edge : graph.get(current)) {
                int neighbor = edge.target;
                int weight = edge.weight;

                // --- RELAXATION STEP ---
                // If a shorter path to neighbor is found through current,
                // update the distance and push neighbor into the queue
                if (dist[current] != Integer.MAX_VALUE
                        && dist[current] + weight < dist[neighbor]) {

                    dist[neighbor] = dist[current] + weight;
                    pq.add(neighbor); // Reconsider neighbor with improved distance
                }
            }
        }

        // Output final shortest distances
        for (int i = 0; i < n; i++) {
            System.out.println("Distance from source(" +  source+ ") to " + i + " is " + dist[i]);
        }
    }

    public static void main(String[] args) {
        int n = 4;

        // Initialize adjacency list
        List<List<Edge>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            graph.add(new ArrayList<>());
        }

        // Add directed edges
        graph.get(0).add(new Edge(1, 4));
        graph.get(0).add(new Edge(2, 2));
        graph.get(2).add(new Edge(1, 1));
        graph.get(1).add(new Edge(3, 5));
        graph.get(2).add(new Edge(3, 8));
        

        graph.get(1).add(new Edge(0, 4));
        graph.get(2).add(new Edge(2, 2));
        graph.get(1).add(new Edge(2, 1));
        graph.get(3).add(new Edge(1, 5));
        graph.get(3).add(new Edge(2, 8));
        
        
        // source
        int src = 3;

        // Execute Dijkstra from vertex 0
        dijkstra(graph, src);
    }

}

```

------

## Behind-the-Scenes Explanation

The priority queue ensures that the next vertex processed is always the closest one not yet finalized.

Relaxation does the real work:

- It compares current knowledge (`dist[v]`) with a newly discovered path
- It replaces inferior paths immediately
- It pushes updated vertices back into contention

### Key Point

Dijkstra’s Algorithm is not about exploring everything. It is about rejecting most paths quickly and refining the few that matter.

------

## Common Mistakes and Debugging Problems

### Common Mistake

Using Dijkstra’s Algorithm with negative weights.

This will silently produce incorrect results.

### Debugging Note

If a node’s distance improves after being marked visited, your implementation is broken.

### Common Mistake

Forgetting the infinity guard:

```java
if (dist[current] != Integer.MAX_VALUE)
```

Without it, integer overflow can corrupt results.

------

## Comparison to Related Ideas

### Comparison: Dijkstra vs Bellman-Ford

| Feature          | Dijkstra    | Bellman-Ford |
| ---------------- | ----------- | ------------ |
| Negative weights | Not allowed | Allowed      |
| Performance      | Fast        | Slower       |
| Cycle detection  | No          | Yes          |

### Insight

Dijkstra trades flexibility for speed. Bellman-Ford tolerates chaos but pays for it.

------

## Best Practices

- Use adjacency lists for scalability
- Always validate edge weights
- Prefer priority queues over manual scans
- Separate graph construction from algorithm logic
- Keep relaxation logic explicit and readable

------

## Key Terms

- Graph
- Vertex
- Edge
- Weight
- Shortest Path
- Relaxation
- Priority Queue
- Greedy Algorithm

------

## Chapter Summary

Dijkstra’s Algorithm is a precise instrument. It builds shortest paths by repeatedly applying relaxation and committing to the best-known option. Its correctness depends on a single assumption: no negative weights.

Break that assumption, and the algorithm doesn’t complain—it deceives.

Use it with discipline.

------

## Review Questions

1. What does relaxation do?
   A. Removes edges
   B. Updates shortest distances
   C. Sorts vertices
   D. Adds cycles
2. What condition must hold for correctness?
   A. Graph must be complete
   B. No negative edge weights
   C. Graph must be undirected
   D. Must use recursion
3. What structure selects the next vertex?
   A. Stack
   B. Queue
   C. Priority Queue
   D. Array
4. When is a node finalized?
   A. When added to queue
   B. When visited
   C. When initialized
   D. When relaxed
5. What happens if negative weights exist?
   A. Algorithm fails loudly
   B. Algorithm returns wrong results
   C. Algorithm slows down
   D. No change
6. What is stored in dist[]?
   A. Edge counts
   B. Parent nodes
   C. Shortest distances
   D. Vertex labels
7. Which algorithm handles negative weights?
   A. BFS
   B. DFS
   C. Bellman-Ford
   D. Prim’s
8. What triggers a relaxation update?
   A. Larger distance found
   B. Equal distance found
   C. Smaller distance found
   D. Random condition

------

## Answer Key

1. B
2. B
3. C
4. B
5. B
6. C
7. C
8. C

------

## Glossary

**Graph** – A set of vertices connected by edges
**Vertex** – A node in a graph
**Edge** – A connection between vertices
**Weight** – Cost assigned to an edge
**Shortest Path** – Minimum total weight path
**Relaxation** – Updating a vertex’s shortest distance if a better path is found
**Priority Queue** – Structure that retrieves the minimum element efficiently
**Greedy Algorithm** – Makes locally optimal decisions at each step

------

## Final Takeaway

Relaxation is not a detail—it is the algorithm. Every correct implementation rises or falls on that single comparison. Everything else is scaffolding.
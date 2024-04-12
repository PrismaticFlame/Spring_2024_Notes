---
aliases:
  - Breadth-First Search
---
Breadth First Search (BFS) is a fundamental graph traversal algorithm used to explore the vertices of a graph systematically. BFS starts at a designated "root" vertex and explores all the vertices that are reachable from it, level by level, in a breadthward motion. It visits all the neighbors of a vertex before moving on to the neighbors' neighbors.

### Key Characteristics of BFS:

1. **Queue-based Approach:**
   - BFS employs a queue data structure to keep track of vertices that need to be visited. The queue initially contains only the root vertex. As BFS explores the graph, it adds adjacent vertices to the queue for subsequent exploration.

2. **Level-by-Level Exploration:**
   - BFS explores the vertices of the graph in level-by-level order. It starts at the root vertex (level 0) and visits all vertices at level 1 before moving on to vertices at level 2, and so on. This ensures that vertices closer to the root are visited before vertices further away.

3. **Visited Marking:**
   - BFS marks each visited vertex to avoid revisiting vertices that have already been explored. This prevents infinite loops in graphs with cycles and ensures that BFS terminates after visiting all reachable vertices.

4. **Optimality:**
   - BFS guarantees that it will find the shortest path from the root vertex to any other vertex in an unweighted graph. This property makes BFS suitable for tasks such as finding the shortest path, checking for connectivity, and exploring the structure of a graph.

5. **Applications:**
   - BFS has various applications in computer science and beyond, including finding the shortest path in unweighted graphs, testing for bipartiteness, computing connected components, and network routing.

### Algorithm Steps:

1. Enqueue the root vertex into the queue and mark it as visited.
2. While the queue is not empty:
   - Dequeue a vertex from the front of the queue.
   - Visit the dequeued vertex and process it.
   - Enqueue all unvisited neighbors of the dequeued vertex into the queue and mark them as visited.
3. Repeat step 2 until the queue is empty.

### Example:

Consider the following graph:

```
    A
   / \
  B   C
 / \ / \
D  E F  G
```

Starting from vertex A, the BFS traversal would visit the vertices in the order: A, B, C, D, E, F, G.

### Advantages and Limitations:

- **Advantages:**
  - BFS is simple to implement and understand.
  - It guarantees the shortest path in unweighted graphs.
  - It can be used to find all connected components in a graph.

- **Limitations:**
  - BFS may consume a lot of memory when dealing with large graphs due to the need to store all visited vertices in a queue.
  - It does not perform well on graphs with high branching factors or long paths.

BFS is a versatile algorithm used in various domains, including computer science, robotics, and network analysis. In robotics, BFS can be employed for tasks such as exploring unknown environments, mapping, and navigation planning.
Certainly! Depth First Search (DFS) is another fundamental graph traversal algorithm used to explore the vertices of a graph systematically. Unlike Breadth First Search (BFS), which explores vertices level by level in a breadthward manner, DFS explores vertices depthward, visiting as far as possible along each branch before backtracking.

### Key Characteristics of DFS:

1. **Stack-based Approach:**
   - DFS employs a stack data structure (or recursion) to keep track of vertices that need to be visited. It starts at a designated "root" vertex and explores as far as possible along each branch before backtracking.

2. **Depthward Exploration:**
   - DFS explores the vertices of the graph depthward, meaning it visits vertices along a branch until it reaches a dead end (i.e., a vertex with no unvisited neighbors). It then backtracks to the most recent unexplored vertex and continues the exploration.

3. **Marking Visited Vertices:**
   - DFS marks each visited vertex to avoid revisiting vertices that have already been explored. This prevents infinite loops in graphs with cycles and ensures that DFS terminates after visiting all reachable vertices.

4. **Recursion or Iteration:**
   - DFS can be implemented using either recursion or iteration. In the recursive approach, each recursive call explores a neighboring vertex, while in the iterative approach, a stack is used to keep track of vertices to be explored.

5. **Applications:**
   - DFS has various applications in computer science and beyond, including finding connected components, topological sorting, cycle detection, and solving puzzles and mazes.

### Algorithm Steps (Recursive Approach):

1. Visit the starting vertex and mark it as visited.
2. Recursively explore each unvisited neighbor of the current vertex.
3. If all neighbors have been visited, backtrack to the previous vertex and continue exploration from there.
4. Repeat steps 2-3 until all reachable vertices have been visited.

### Example:

Consider the following graph:

```
    A
   / \
  B   C
 / \ / \
D  E F  G
```

Starting from vertex A, the DFS traversal would visit the vertices in the order: A, B, D, E, C, F, G.

### Advantages and Limitations:

- **Advantages:**
  - DFS is simple to implement and understand.
  - It requires less memory compared to BFS because it explores vertices depthward instead of storing them in a queue.
  - It is well-suited for certain tasks, such as topological sorting and cycle detection.

- **Limitations:**
  - DFS may not find the shortest path in general graphs.
  - It can get stuck in infinite loops if not properly implemented or if the graph has cycles.
  - The order in which vertices are visited depends on the specific implementation, which may not be optimal for certain applications.

DFS is a versatile algorithm used in various domains, including computer science, robotics, and artificial intelligence. In robotics, DFS can be employed for tasks such as exploring unknown environments, mapping, and planning paths in maze-like structures.
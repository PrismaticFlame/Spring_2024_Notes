Greedy search, also known as greedy best-first search, is a heuristic-based graph search algorithm that explores a graph by always selecting the most promising vertex based on a heuristic function. Unlike Breadth First Search (BFS) and Depth First Search (DFS), which systematically explore all reachable vertices, greedy search prioritizes vertices that appear to be closest to the goal according to the heuristic function.

### Key Characteristics of Greedy Search:

1. **Heuristic Function:**
   - Greedy search relies on a heuristic function that estimates the "closeness" of each vertex to the goal. The heuristic function provides an optimistic estimate of the cost or distance from a vertex to the goal, typically based on problem-specific knowledge or domain expertise.

2. **Priority Queue:**
   - Greedy search maintains a priority queue of vertices ordered by their heuristic values. Vertices with lower heuristic values (i.e., closer to the goal) are given higher priority and explored first.

3. **Local Optimality:**
   - Greedy search makes locally optimal decisions at each step by selecting the vertex that appears to be the most promising based on the heuristic function. It does not consider the global structure of the graph or potential future costs.

4. **Incomplete and Non-Optimal:**
   - Greedy search is incomplete and may not find a solution if it gets stuck in a dead end or a local minimum. Additionally, it is not guaranteed to find the optimal solution, as it may overlook shorter paths in favor of vertices with lower heuristic values.

5. **Applications:**
   - Greedy search is commonly used in various domains, including artificial intelligence, optimization problems, and pathfinding. It is particularly useful for problems where finding an approximate solution quickly is more important than finding the optimal solution.

### Algorithm Steps:

1. Initialize the priority queue with the start vertex and its heuristic value.
2. While the priority queue is not empty:
   - Dequeue the vertex with the lowest heuristic value from the priority queue.
   - If the dequeued vertex is the goal, terminate with success.
   - Otherwise, expand the dequeued vertex by exploring its neighbors and enqueue them into the priority queue with their heuristic values.
3. Repeat step 2 until either the goal is found or the priority queue is empty.

### Advantages and Limitations:

- **Advantages:**
  - Greedy search is computationally efficient and requires minimal memory overhead.
  - It can find solutions quickly, especially in domains where heuristics provide accurate estimates.
  - Greedy search can be easily adapted to different problem domains by modifying the heuristic function.

- **Limitations:**
  - Greedy search may get stuck in local minima or dead ends, leading to incomplete solutions.
  - It does not guarantee the optimality of the solution and may overlook shorter paths in favor of vertices with lower heuristic values.
  - Greedy search is sensitive to the quality of the heuristic function and may produce suboptimal results if the heuristic is inaccurate.

Greedy search is a valuable tool in various applications, including pathfinding in robotics, optimization problems, and artificial intelligence. In robotics, greedy search can be applied for tasks such as motion planning, pathfinding in grid-based environments, and navigation in known or partially known environments. However, it is important to consider its limitations and potential drawbacks when applying it to real-world problems.
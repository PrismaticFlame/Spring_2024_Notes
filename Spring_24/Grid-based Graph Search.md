Grid-based graph search is a category of pathfinding algorithms used in robotics and artificial intelligence for planning paths in environments represented as grid maps. In grid-based graph search, the environment is discretized into a grid of cells, where each cell represents a specific location or region. The robot's motion is constrained to move between adjacent grid cells, and the goal is to find a path from a start cell to a goal cell while avoiding obstacles.

### Types of Grid-Based Graph Search Algorithms:

1. **[[Dijkstra's Algorithm]]:**
   - Dijkstra's algorithm is a classic graph search algorithm that finds the shortest path from a start node to all other nodes in a weighted graph. In the context of grid-based graph search, Dijkstra's algorithm can be applied by treating each grid cell as a node and computing the shortest path between them while considering the grid cell's connectivity and obstacles.

2. **[[A-star Search|A*]] Algorithm:**
   - A* (pronounced "A-star") is a popular and widely used pathfinding algorithm that combines elements of Dijkstra's algorithm and heuristic search. A* is more efficient than Dijkstra's algorithm for finding paths in grid-based environments because it uses a heuristic function to guide the search towards the goal while also considering the actual cost of reaching each grid cell.

3. **[[Breadth First Search|Breadth-First Search]] (BFS):**
   - BFS is a simple graph traversal algorithm that explores all neighboring nodes of a given node before moving on to the next level of nodes. In the context of grid-based graph search, BFS can be used to find the shortest path from a start cell to a goal cell by systematically exploring the grid in breadth-first order.

4. **[[Depth First Search|Depth-First Search]] (DFS):**
   - DFS is another graph traversal algorithm that explores as far as possible along each branch before backtracking. While DFS is not typically used for finding shortest paths in grid-based environments due to its lack of optimality, it can be useful for exploring all reachable cells from a given start cell.

5. **[[Greedy (Best First) Search|Greedy Best-First Search]]:**
   - Greedy Best-First Search is a heuristic search algorithm that always expands the node with the lowest heuristic value. In the context of grid-based graph search, Greedy Best-First Search uses a heuristic function that estimates the distance from each cell to the goal and expands cells accordingly.

6. **[[Theta-star Algorithm|Theta* Algorithm]]:**
   - Theta* is an improvement over A* that optimizes pathfinding by considering the line of sight between nodes. Theta* reduces the number of nodes expanded by A* by skipping unnecessary nodes that lie along straight paths.

### Advantages and Limitations:

- **Advantages:**
  - Grid-based graph search algorithms are conceptually simple and easy to implement.
  - They can handle environments with obstacles and constrained motion.
  - Many grid-based graph search algorithms guarantee optimality when certain conditions are met.

- **Limitations:**
  - Grid-based graph search algorithms may suffer from high memory and computational requirements, especially in large grid maps.
  - They may not be suitable for continuous environments or environments with complex geometry.
  - Some algorithms, such as BFS and DFS, may not be optimal in terms of path length.

Grid-based graph search algorithms are commonly used in robotics for tasks such as robot motion planning, pathfinding for autonomous vehicles, and navigation in grid-based maps or environments. The choice of algorithm depends on factors such as the size and structure of the grid, computational resources, and the desired optimality of the path.
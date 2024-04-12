---
aliases:
  - Uniform Cost Search
---
Dijkstra's algorithm is a classic and widely used graph search algorithm that finds the shortest path from a designated start node to all other nodes in a weighted graph. It was conceived by computer scientist Edsger W. Dijkstra in 1956 and is commonly employed in various applications, including routing in computer networks, pathfinding in robotics, and navigation in maps.

### Key Features of Dijkstra's Algorithm:

1. **Single-Source Shortest Path:**
   - Dijkstra's algorithm is a single-source shortest path algorithm, meaning it computes the shortest path from a single source node (the start node) to all other nodes in the graph.

2. **Weighted Graphs:**
   - Dijkstra's algorithm is designed to handle graphs with non-negative edge weights. Each edge in the graph represents a connection between two nodes, and the weight of the edge indicates the cost or distance associated with traversing that edge.

3. **Priority Queue:**
   - Dijkstra's algorithm uses a priority queue to select the next node to visit during the traversal. The priority queue stores nodes along with their tentative distances from the start node. Nodes with smaller tentative distances are given higher priority.

4. **Greedy Approach:**
   - Dijkstra's algorithm employs a greedy approach by iteratively selecting the node with the smallest tentative distance and exploring its neighboring nodes. It continuously updates the tentative distances to neighboring nodes based on the current shortest path found.

5. **Visited Nodes:**
   - As Dijkstra's algorithm traverses the graph, it keeps track of which nodes have been visited and which nodes are yet to be visited. Once a node is visited, its tentative distance is finalized, and further exploration from that node is unnecessary.

6. **Optimality:**
   - Dijkstra's algorithm guarantees the shortest path from the start node to any other node in the graph when all edge weights are non-negative. However, it may not produce correct results if negative edge weights are present.

### Algorithm Steps:

1. Initialize all nodes with a tentative distance of infinity, except the start node, which has a tentative distance of 0.
2. Add the start node to the priority queue.
3. While the priority queue is not empty:
   - Extract the node with the smallest tentative distance from the priority queue.
   - For each neighbor of the extracted node:
     - Calculate the tentative distance to the neighbor through the current node.
     - If the calculated tentative distance is smaller than the neighbor's current tentative distance, update the neighbor's tentative distance and add it to the priority queue.
4. Repeat step 3 until all nodes have been visited.

### Advantages and Limitations:

- **Advantages:**
  - Dijkstra's algorithm is simple to understand and implement.
  - It guarantees the shortest path from the start node to all other nodes in the graph.
  - It can handle graphs with non-negative edge weights efficiently.

- **Limitations:**
  - Dijkstra's algorithm may not perform optimally in graphs with negative edge weights.
  - It may require a significant amount of memory and computation for large graphs.
  - The algorithm does not scale well for graphs with many nodes and edges.

Despite its limitations, Dijkstra's algorithm remains a fundamental tool in graph theory and computer science, and it serves as the basis for many other pathfinding algorithms and optimization techniques. In robotics, Dijkstra's algorithm is often used for motion planning, pathfinding in grid-based maps, and navigation in complex environments.
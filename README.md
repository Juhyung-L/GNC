# dynamic_obstacle_avoidance
This repository has two packages: A* Search global path planner and Dynamic Window Approach (DWA) local path planner.

Detailed Explanation at: https://juhyungsprojects.blogspot.com/2024/04/dynamic-window-approach-for-local-path.html

# A* Search Global Path Planner:
The A* Search global path planner finds the shortest trajectory from the robot's current pose to the goal pose using the static global costmap and the A* Search algorithm. The algorithm is a modified Breath-First Search algorithm where a priority queue is used instead of a regular queue. The priority queue sorts the inserted nodes based on their heuristics.The heuristics in this case is the sum of three components:
- Distance between the current node and the goal node
- Distance between the current node and the start node
- Occupancy value of the current node

Every time a node is inserted into the priority queue, the node with the lowest priority comes at the top and is therefore popped first. Intuitively, this means that nodes that are both closer to the goal and obstacle-free are searched first when looking for the shortest trajectory.

https://github.com/Juhyung-L/GNC/assets/102873080/6edecccf-5511-4af7-8c7a-431e26509217

# DWA Local Path Planner
The DWA local path planner samples a bunch of local trajectories (short trajectories) that the robot can follow. The sampled trajectories are scored by multiple critics and the trajectory with the highest score is chosen. There are 3 critics implemented in this repository: GlobalPathAlignCritic, HomingCritic, ObstacleProximityCritic.

GlobalPathAlignCritic:
- Penalizes trajectories that do not align with the global trajectory.

HomingCritic:
- If the goal pose is inside the local costmap, score local trajectories based on distance between goal pose and last pose of local trajectory

ObstacleProximityCritic:
- Penalizes trajectories that too are close to obstacles

[![Watch the video](https://img.youtube.com/vi/XEWZgA5ivXk/maxresdefault.jpg)](https://www.youtube.com/watch?v=XEWZgA5ivXk "DWA Local Planner Footage")

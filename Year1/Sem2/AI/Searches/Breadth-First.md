Breadth-first search is one of the most common search strategies:
- The nood node is expanded first
- Then all successors of the root node are expanded, and then successors of these
- This loops until goal state is reached

It is an [[Uninformed]] search algorithm

The frontier nodes that are expanded belong to a given depth of the tree

This is equivalent to expanding the shallowest unexpanded node in the frontier; we use a queue for expansion. Once a goal state is added to the frontier queue, we stop the search

[[Performance]]:
- Completeness - If goal node is in tree then BFS is complete as it will find it
- Optimality - BFS is optimal id all actions have the same cost
- Time complexity - $O(b^d)$
- Space complexity - $O(b^{d-1})$





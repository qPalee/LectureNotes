We can evaluate the performance of an algorithm based on:
- Completeness - is it guaranteed to find a solution given one exists
- Optimality - is it able to find optimal solution
- Time complexity - time taken to find solution
- Space complexity - memory needed too perform search

To measure the performance, the size of the space graph is typically used, i.e., |V| + |ℰ|, the set of vertices and set of edges, respectively

In AI, we use an implicit representation of the graph via the initial state, actions and transition model (as the graph could be infinite)

Therefore, the following three quantities are used:  
• Branching factor, the maximum number of successors of each node: 𝑏  
• Depthof the shallowest goal node (number of steps from the root): 𝑑  
• The maximum lengthof any path in the state space: 𝑚


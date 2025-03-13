# Distributed Systems

Each problem we study in distributed systems will have an enumerated set of requirements that any solution we design must satisfy

These requirements form our <span style="color:#00bfff">problem specification</span>
- This is covered in [[Year3/Sem2/dads/concepts/overview|overview]]

### Synchronous Network Model
Extent of message delays and execution speed are known and bounded

- They can be represented as a directed graph $G = V, E)$ with a fixed message alphabet $M$
- The edges and number of nodes may or may not be known to each node
- Out-degree/in-degree are the number of edges leaving/entering a node respectively
- Distance between nodes is the shortest path between them (A* algorithm)
- Diameter of a graph is the maximum distance between any two nodes in the graph
	- Distance of the two furthest away nodes


For each node $i \in V$ there is a process which formally consists of:
- $\textcolor{#00bfff}{states_i}$ - Set of states, not always finite
- $\textcolor{#00bfff}{start_i}$ - Non-empty subset of states
- $\textcolor{#00bfff}{msgs_i}$ - Message generation function
	- Specifies the message that process $i$ sends to a neighbour, starting from the given state
- $\textcolor{#00bfff}{trans_i}$ - State transition function
	- Specifies the new state to which process $i$ should move

For each $(i, j) \in E$ there is a channel which can hold a single message $M$

Processes repeatedly perform two actions in lock-step:
- Apply the message generation function to the current state to generate the messages to be sent to its neighbours
- Apply the state transition function to the current state and the incoming messages to obtain the new state

#### What can go wrong?
We can account for process failures and channel failures
- <span style="color:#00bfff">Link failure</span> - A channel can fail by losing messages
- <span style="color:#00bfff">Stop failure</span> - A process can just stop somewhere in the middle of its execution
- <span style="color:#00bfff">Byzantine failure</span> - A process can generate its next messages and state in some arbitrary way
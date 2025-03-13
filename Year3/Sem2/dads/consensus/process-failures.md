# Distributed Consensus With Process Failures

### The problem
Assume $N$ indexed processes arranged in a connected, undirected graph
- Each process knows the entire graph
- Each process value starts from a fixed value set $V$
- We can assume the synchronous network model
	- Allowing for failure of at most $f$ processes
	- All messages sent are assumed to be delivered

<span style="color:#00bfff">Aim</span>: All processes eventually output decisions from $V$ by setting their decision state to values from $V$

<span style="color:#00bfff">Agreement</span>: No two processes decide on different values

<span style="color:#00bfff">Validity</span>: If all processes start with the same initial value $v \in V$, then $v$ is the only possible decision value

<span style="color:#00bfff">Termination</span>: All non-faulty processes eventually decide

[[byzantine-failure]] is the same but the agreement changes to include only non-faulty processes

We do this since we cannot impose limitations on what a faulty process might start with or decide

##### Complexity under Byzantine Failure
Time complexity is unaffected
- We can consider the number of rounds under which all non-faulty processes decide

For communication complexity, we can count both the number of messages and amount of communication
- We can only use messages sent by non-faulty processes in the case of byzantine failure
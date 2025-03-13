# Distributed Consensus with Link Failures

### Coordinated Attack Problem
A fundamental problem of reaching consensus in a setting where messages may be lost

- Imagine a number of generals are a coordinated attack from different directions
- The only way for the attack to succeed is for all the generals to commit to attack
- Each general has an initial opinion about whether their army is ready to attack
- Generals can communicate via messengers, who maybe get lost or captured

If all messengers are reliable, then after a number of rounds, all generals will have 

### The problem in Distributed Database Systems
Assume a collection of processes have participated in a database transaction

Each process arrives at an initial view on whether the transaction should be committed or aborted
- A process will want to commit if its involvement is successful, and abort otherwise

Processes communicate and decide whether to commit or abort 

#### Formal Definition
Assume $N$ processes with indexes in an undirected graph
- Each process knows the entire graph
- Each process starts with an input in $\{1, 0\}$
- We can assume the synchronous network model

<span style="color:#00bfff">Aim</span>: All processes to eventually output decisions in $\{1, 0\}$ by setting their decision state components

<span style="color:#00bfff">Agreement</span>: No two processes decide on different values

<span style="color:#00bfff">Validity</span>: If all processes start with $n$, then the only decision value should be $n$ assuming all messages are delivered

<span style="color:#00bfff">Termination</span>: All processes eventually decide

#### Proving the Impossibility

We show for a two node graph, which then extends to $N$

For this we need to understand the definition of **execution** and **indistinguishable** in the synchronous network model

A state assignment of a system is defined to be an assignment of a state in each process

A message assignment is an assignment of a message to each channel

An <span style="color:#00bfff">execution</span> of the system is an infinite sequence $C_0, M_1, N_1, C_1, ...$ where each $C_r$ is a state assignment and each $M_r$ and $N_r$ is a message assignment

If $\alpha$ and $\alpha'$ are two executions, then $\alpha$ is <span style="color:#00bfff">indistinguishable</span> from $\alpha'$ wrt process $i$ if $i$ has:
- the same sequence of states
- the same sequence of outgoing messages
- the same sequence of incoming messages 
in $\alpha$ and $\alpha'$

This is denoted by $\alpha \sim^i \alpha'$ 

##### Impossibility for two nodes
For the proof, we will suppose algorithm $A$ solves the coordinated attack problem on $G$

Assume that for each process there is exactly one start state containing each input value, so the system has one execution for a fixed assignment of inputs

Let $\alpha$ be the execution when both processes start with $1$ and all messages are delivered
- By termination and validity, both eventually decide on value $1$ within $r$ rounds

Let $\alpha_1$ be the same as $\alpha$ except that all messages after the first $r$ rounds are lost

Let $\alpha_2$ be the same as $\alpha_1$ except the last message from process 1 to process 2 is not delivered

Although process 2 may go to a different state after round $r$ in executions $\alpha_1$ and $\alpha_2$, this is never communicated to process 1, therefore $\alpha_1 \sim^i \alpha_2$ 

Consider the execution of $\alpha''$ in which process 1 starts with 1 but process 2 starts with 0 and no messages are delivered
- This means we have $\alpha'' \sim^1 \alpha'$

Consider the execution of $\alpha'''$ in which both processes start with 0 and no messages are received
- This means we have $\alpha''' \sim^2 \alpha''$

In this case Process 2 decides 0 in $\alpha'''$ which is a contradiction of the validity condition

#### Implications of the impossibility
No algorithm can solve the coordinated attack problem

It is possible to solve variations though where messages may be lost
- Relax the problem to tolerate some probability of disagreement
- Possible to obtain upper and lower bounds on the probability of disagreement
- 
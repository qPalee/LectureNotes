# Clocks

Not talking about normal clocks
- Fundamental meaning of time

Time is important for time stamping events
- Mutual Exclusion
- Real time control systems
- Multiprocessor task scheduling

### Big problem with Time
Clocks never remain synchronised, even if all clocks are restarted at the same time
- They drift apart over time

### Terminologies and Concepts
A local physical clock usually provides a time source
- Known as clock time
- Modelled as a function that maps real time into clock time
- Subject to a drift rate $\rho$
- Local clocks are used for local purposes

![[Pasted image 20250313091705.png]]

Clock C is not-faulty during a real time interval $[s, t]$ if it is a monotonic, differentiable function over $[S, T]$ where $C(S) = S$ and $C(t) = T) \ \forall$ $\tau$ between S and T we have
$$1- \frac{\rho}{2} < \frac{dc(T)}{dT} < 1 + \frac{\rho}{2}$$

It follows that
$$1-\rho_2 < \frac{C(t_2) - C(t_1)}{t_2 - t_1} < 1 + \frac{\rho}{2}$$
#### Illustrating drift rate
Definition of non-faulty over a real time interval is essentially reasoning about the bounds of its discrepancy

Over a large enough interval, any drift rate will result in a faulty clock
- Infinite time -> infinite drift

![[Pasted image 20250313092137.png]]

### Types of Local Clock
- <span style="color:#00bfff">Hardware Clocks</span>
	- Physical clock pulses that control circuitry timing within some tolerance
- <span style="color:#00bfff">Logical Clocks</span>
	- Values obtained from hardware clock - counters

These 2 notions coincide when we talk about clock synchronisation in terms of functions and their properties
- This difference relates to the skew of synchronisation $\delta$

### Clock Synchronisation
#### Defining forms of synchronisation
Two clocks $C1$ and $C2$ are said to be $\delta$-synchronised at clock time $t$ if and only if we have $|C1(t) - C2(t)| \leq \delta$

A set of clocks are synchronised if and only if two non-fault nodes are $\delta$-synchronised

To enforce well-synchronised clocks we can:
- Require nodes to read the clocks of other nodes
- Have different mechanisms according to clock implementation
- Make skew be an approximate due to delivery delays


#### How to synchronise
Implement a virtual clock (VC) at each node

A VC, in a similar way to physical clocks, can be modelled as a function that maps real time onto clock time

Clock synchronisation provides a bound for skew and drift rate

We have 2 requirements:
- <span style="color:#00bfff">Agreement</span>
	- Specifies that the skew between all non-faulty nodes is bounded
	- Ensures that there is a sufficiently consistent view of time across all nodes in the system
- <span style="color:#00bfff">Accuracy</span>
	- Ensures that logical clocks keep up with real time



### Revision Tips
Understand concepts like drift and skew
Important that you know definitions
- Diagrams
- Set of clocks being well synchronised
Reliable Time Sources
- Requirements
- Cristians + Berkeley Algorithm
	- Berkeley is more general
Not required to produce the definitional maths but might be easier
- will also accept the explanation of the concept
Logical Clocks - Event ordering
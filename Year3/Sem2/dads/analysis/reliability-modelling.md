# Reliability Modelling
### MTTF
Mean Time to Failure

Expected time a system will operate before first failure

If there are $N$ identical systems which run correctly at $t=0$ but they all fail at time $t_i$ then MTTF has the formula
$$MTTF=\sum^{N}_{i=1}\frac{t_i}{N}$$
In the continuous case, MTTF can be calculated using 
$$MTTF=\int^{\infty}_{0}t \ f(t) \ dt$$ where $f(t)$ is the failure density function - derivative of unreliability

In the case of $\lambda$, this can be reduced down to $$MTTF=\frac{1}{\lambda}$$
### MTTR
Mean Time to Repair

MTTR is the average time to repair a failed computer system
Includes time for detecting and locating the fault, repairing it and reconfiguring the system

It can be difficult to predict analytically
- might require experimental measurement for computation

The repair rate is denoted by $\mu$ 
$$MTTR =\frac{1}{\mu}$$

### MTBF
Mean Time Between Failures

Average time elapsed between failures

It is assumed that after repair, the system works as it was before failure
$$MTBF = MTTR + MTTF$$

### Combinatorial 
Reliability of the system is calculated from the reliability of its components

Construction of a reliability block diagram (RBD) to provide an abstract view of the system

The composition of a RBD is related to the connections between components

Can be modelled in either series or parallel
![[Pasted image 20250210162447.png]]

#### Series Systems
All components are required to work for the overall system to operate correctly

Probabilistic techniques are used to enumerate combinations to ensure a working system

$$P(S_t) = $$

#### Parallel Systems
The failure of one component does not result in a system failure

#### M-of-N systems
Generalisation of parallel systems

Instead of at least one component working, we can assume M out of N components should work 

The reliability of this is expressed as:
$$P(S_t) = \sum^{N-M}_{i=0} \frac{N!}{(N-i)! \ i!}(R(t))^{N-i}(1-R(t)^i$$
which can be rewritten as 
$$P(S_t) = \sum^{N}_{i=M} {}^nC_i \cdot R(t)^i \cdot Q(t)^{N-i}$$

#### Reality
In reality, systems use a combination of all 3 of these

### Cut Set and Tie Sets
#### Cut Sets
Given a reliability block diagram (RBD)

We can draw lines through the diagram to represent combinations of elements in which simultaneous failures would lead to a system failure
- We are interested in the minimal cut sets 
	- subsets of this will not lead to system failure
- Provides a **lower bound on reliability**

In a series system, each cut set is size 1
In a parallel system, each cut set is of size system

#### Tie Sets
They are very similar to cut sets but provide an **upper bound** on reliability instead

The subsets of the minimal tie set will not lead to a working system

"For the lord of fuck revise this"

#### Example - TMR
Three processors (components) run in parallel - outputs are compared and discrepancies indicate a fault

At least 2 of the 3 must work correctly

Assume each processor has a failure rate $\lambda$
Reliability of each processor is $e^{-\lambda t}$

Using the expression from M-of-N systems, the reliability of TMR is:
![[Pasted image 20250210164021.png]]

The MTTF of TMR is $\frac{5}{6\lambda}$

### Markov Models
**Slides here**
#### Continuous Time Markov Chains
They have two components:
- <span style="color:#00bfff">State</span> - Comprise all that is needed to characterise it
- <span style="color:#00bfff">State Transition</span> - Govern how changes in the state will occur

##### Example
![[Pasted image 20250210164814.png]]

###### TMR for Markov Chains
Three replicas are run in parallel on the same input, with the outputs being compared

At least two nodes must be up for successful operation
![[Pasted image 20250210165054.png]]

We start at `111` in a state in which nothing has failed
If nothing fails we stay in `111`
If something fails we transition to a different node

###### Condensed Continuous Time Markov Chains
![[Pasted image 20250213092928.png]]

Split the nodes into groups of 3:
- all nodes are up
- two nodes are up
- the whole system is down (failure)

###### Calculating Model Probabilities
Assuming a failure rate of $\lambda$ and the exponential failure law, the probability of a model failure at time $t + \Delta t$ given it was working at $t$ is
$$1-\frac{R(t - \Delta t)}{R(t)} = 1-\frac{e^{-\lambda (t - \Delta t)}}{e^{-\lambda t}} = \textcolor{#00bfff}{1-e^{-\lambda \Delta t}}$$
###### Solving the model
<span style="color:#ff0000">Don't need to be able to solve the model</span>

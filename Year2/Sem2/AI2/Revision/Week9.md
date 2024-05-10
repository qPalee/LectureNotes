# Week 9
## Solving CSPs

### Systematical Search
#### Generate and Test
The exhaustive generate-and-test algorithm is to generate all the complete assignments, then test them all in turn and return the first one that satisfies all constraints

It needs to store all $d^n$ complete assignments, where $d$ is the domain size and $n$ is the number of variables

This is very inefficient so we must find alternatives

### Standard Search Formulation
In CSPs, states are defined by the values assigned so far
- Initial State: the empty assignment {}
- Successor function: Assign a value to an unassigned variable
- Goal: The current assignment is complete and satisfies all constraints

#### Solving CSPs with BFS
Example:
There are 3 variables {A,B,C}, all with domain {0, 1, 2}. The constraint is A+B+C=1. 
Since all the solutions are always in the bottom layer, BFS needs to traverse all the nodes
![[Pasted image 20240505121542.png]]

#### Solving CSPs with DFS
Example: 
There are 3 variables {A,B,C}, all with domain {0, 1, 2}. The constraint is A+B+C=1. 
Sounds like a good idea but what if the constraint is $A<B<C$
![[Pasted image 20240505122151.png]]

#### Checking constraints as you go
Example:
There are 3 variables {A,B,C}, all with domain {0, 1, 2}. The constraint is $A<B<C$.
Consider only values which do not conflict with past assignments
May have to do some computation to check the constraints such as 'incremental goal test'

#### Backtracking
Example: There are 3 variables A, B, C al with domain {0, 1, 2}. The constraint is $A<B<C$
![[Pasted image 20240505122620.png]]

##### Improving backtracking
General purpose ideas can give a huge boost in speed

###### Filtering
Can we detect inevitable failure early on?

Keep track of domains for unassigned variables and cross off bad options. 

Forward Checking:
When we assign a variable, cross of anything that is now violated on all its neighbours' domains

Example:
There are 3 variables A, B, C with domain {0, 1, 2}. The constraint is $B>A>C$

When A is assigned the value 0 ($A=0$), domains of its neighbours B and C are reduced, and we can tell this assignment is not legal since the domain of C is now empty
![[Pasted image 20240505123557.png]]

###### Ordering
Which variable should be assigned next?

Consider the minimum number of remaining values - <span style="color:#00bfff">choose the variable with the fewest legal values left in its domain</span>


Example: There are 3 variables A, B, C all with domain {0, 1, 2}. The constraint is $A \leq B \lt C$. 

Once A is assigned 0 ($A=0$), after forward checking C will be assigned since its domain is smaller than B's domain
![[Pasted image 20240505123543.png]]


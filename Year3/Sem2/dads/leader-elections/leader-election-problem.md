# The Leader Election Problem
Has its origin in token ring networks
![[Pasted image 20250217161612.png]]

in each turn, each process holds a token, and then can send messages on the network

There are several variants of the problem:
- Ring could be unidirectional or bidirectional
- Number of processes may be unknown
- Non-leaders need to know they are not the leader

#### Specification
We know that a spec can be broken down into parts:
- Safety - "Nothing bad happens"
- Liveness - "Sometimes something good will happen"

For the leader election, this translates to:
<span style="color:#00bfff">Safety</span>
- At any one time, there is at most one leader in the system
<span style="color:#00bfff">Liveness</span>
- Sometimes there exists a leader in the system

In a synchronous system, we can take 'sometimes' to mean within a time bound
- Worse case this can mean eventually

### Leader Election in a Token Ring
Assumptions:
- Network is a connected ring
- Nodes habe consecutive unique identifiers $0, 1, ... , n-1$
- Each node knows its left and right neighbour
	- It can only communicate with one of them
- Addition is modulo $N$

#### LCR Algorithm
- Each process sends its identifier around the ring
- When a process receives an identifier, it compares that identifier to its own
- If the identifier is:
	- Greater than its own, it passes it on
	- Less than its own, it discards it
	- Equal to its own, the process declares itself the leader

##### Pseudocode example

For each $i$:
- the message generation function $msgs_i$ is to send the current value of $send$ to the process $i+1$

- the transition function $trans_i$ is
```
send = null
if(incoming_message (v) is UID):
	case:
		v > u: send = v;
		v = u: status = leader;
		v < u: break;
```
##### Proving Liveness
Either no correct process exists or a process is eventually elected leader

It is trivial to show that there will be no leader if there is no correct process

To prove liveness for $n>0$ processes, we need to show that process $i_{max}$ becomes leader by the end of round $n$ 
##### Proving Safety
At any one time, there is at most one leader

We need to shoe that no other process other than $i_{max}$ ever outputs the value 'leader'

##### Complexity Analysis
It takes $n$ rounds before a leader is elected
$\therefore$ message complexity is $O(n^2)$

Time complexity is $O(n)$

#### HS Algorithm
HS is the first algorithm with $O(n \ log n)$ communication complexity
- Ring size can be unknown
- Bidirectional communication

![[Pasted image 20250220092920.png]]

Each process $i$ operates in phases

In each phase $l$, process $i$ send out 'tokens' containing its identifier $u_i$ in each direction

These are intended to travel distance $2^l$ before returning to their origin

If both tokens make it back safely then process $i$ continues with the following phase

If both tokens make it back safely then process $i$ continues to the next phase

##### Basic logic
While a token is proceeding in the outbound direction, each other process $j$ on the path compares $u_i$ with its own identifier $u_j$
- If $u_i < u_j$ then $j$ discards the token
- If $u_i > u_j$ then $j$ relays $u_i$
- If $u_i == u_j$ then $j$ has received its own identifier without it turning around, $\therefore j$ elects itself leader

##### Formal Definiton
$M$ is the set of triples consisting of <identifier, direction-flag, hop-count>

For each $i$, the state in $states_i$ are:
- $u$, a unique identifier
- $send+$, containing either an element of $M$ or $null$ (initially <$u_i$, out, 1>)
- $send-$, containing either an element of $M$ or $null$ (initially <$u_i$, out, 1>)
- $status$, with values in $\{unknown, leader\}$ (initially $unknown$)
- $phase$, a non-negative integer (initially $0$)

##### Complexity Analysis


<span style="color:#ff0000">TimeSlice and VariableSpeeds will **not** be on the exam</span>

### Leader Election in a General Network


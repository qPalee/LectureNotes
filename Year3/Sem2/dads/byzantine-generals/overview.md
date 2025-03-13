# Byzantine Generals

<span style="color:#00fc00">VERY IMPORTANT WILL VERY LIKELY BE ON THE EXAM</span>

need to define these fuckers + explanation
![[Pasted image 20250310160747.png]]

This is in a synchronous network

### Impossibility Result

### Oral Message Solution

### Signed Message Solution

### Practical Byzantine Fault Tolerance
Like a 25ish% chance itll be on the exam apparently

### FPL Impossibility
I'll remember it better if I call it this

We're going asynchronous

'we are all processes you are going to respond eventually'

In the context of an asynchronous network, there is no deterministic consensus algorithm for that network if there is one or more crashes

Impossibility means we can not simultaneously provide safety, liveness, asynchrony AND fault tolerance
- you can only have 3 of the 4
- in an asynchronous network we can design for safety and liveness but we can’t tolerate faults

Impossibility does NOT mean that the distributed consensus problem can not be solved in general


#### Consensus Properties in Partially Synchronous Networks
VERY IMPORTANT SLIDE


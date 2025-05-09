# Reliable Broadcast Algorithms

There are 5 different algorithms
<span style="color:#00bfff">Best Efforts Broadcast</span>
- Guarantees reliable delivery depending on correctness of sender process

<span style="color:#00bfff">Reliable Broadcast</span>
- Guarantees independent of sender process

<span style="color:#00bfff">Uniform Reliable Broadcast</span>
- Ensures delivery also for faulty processes (where possible)

<span style="color:#00bfff">FIFO Reliable Broadcast</span>
- Reliable broadcast with FIFO delivery order

<span style="color:#00bfff">Casual Reliable Broadcast</span>
- Reliable broadcast with 'global FIFO' delivery order

### Intuition
Broadcast is useful in applications where some processes subscribe to events published by other processes

Subscribers might require some reliability guarantees from the broadcast service that the underlying network does not provide

### Best Efforts Broadcast
#### Events
Request: $<BEBBroadcast, m>$
Indication: $< BEBDeliver, src, m>$
#### Properties
<span style="color:#00bfff">Validity</span>
- If $p_i$ and $p_j$ are correct then every message broadcast by $p_1$ is eventually delivered by $p_j$
<span style="color:#00bfff">No duplication</span>
- No message is delivered more than once
<span style="color:#00bfff">No creation</span>
- No message is delivered unless it was broadcast


Reliable delivery only if both sender and receiver are correct

#### Algorithm
![[Pasted image 20250327092451.png]]

### Reliable Broadcast
If the sender fails, we still want to be able to finish broadcasting

RB has the same properties as BEB with one more
<span style="color:#00bfff">Agreement</span>
- For any message $m$, if a correct process delivers $m$, every correct process delivers $m$


![[Pasted image 20250327093144.png]]
^This should say $m_1$^

![[Pasted image 20250327093633.png]]

Despite $p_1$ failing, both $p_2$ and $p_3$ still deliver

Only correct processes are required to agree
- Faulty processes can do whatever the fuck they want

![[Pasted image 20250327093818.png]]

Worst case this has $N^2$ message complexity

### Uniform Reliable Broadcast
The properties are the same as BEB apart from one
<span style="color:#00bfff">Uniform Agreement</span>
- For any message $m$, if a process delivers $m$, every correct process delivers $m$

URB is basically a coping algorithm

### FIFO Broadcast
Enforces a strict ordering amongst messages
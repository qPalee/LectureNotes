# Generic Clock Synchronisation Protocol

Any protocol will comprise of 3 parts
- generation of an event to trigger resynchronisation
- assignment of time
- introduction of an adjustment to that

### Resynchronisation Event Detection

One way to implement this used approximately synchronised clocks

For some predefined value $R$, each node $p$ waits until $VC_p^j$ reads $jR$ before starting $VC_p^{j+1}$

Another way to implement event detection is for each node to broadcast a message when its CV reaches some predefined value and to resent when such a message has been received by any correct node

### Reading current real time
We need to read $N$ clock values simultaneously, which is not possible in a distributed system

A possible approach is to:
- Have each node locally implement approximate VC at other nodes
- Node $p$ maintains a collection of table $\$ which can be used to compute an approximation for $VC_q^j(t)$ and blah blah blah

<span style="color:#ff0000">Finish this</span>
### Convergence Functions

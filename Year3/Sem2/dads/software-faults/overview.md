# Software Fault Tolerance

"Today we will do things of use"

Given a specification $SPEC$, a program $P$ that satisfies $SPEC$ and a fault model $F$

Consider the fault model $F$ to be a function that transforms $P$ into a program $P' = F(P)$
$P'$ is said to be $F$-tolerant if $P'$ satisfies $SPEC$

We know that a system specification consists of two parts:
- Safety
- Liveliness

If $P'$ only satisfies **safety** in the presence of $F$, then $P'$ is said to be <span style="color:#00bfff">fail-safe F-tolerant</span>
If $P'$ only satisfies **liveliness** in the presence of $F$, then $P'$ is said to be <span style="color:#00bfff">non-masking F-tolerant</span>
If $P'$ does not satisfy either of them in the presence of $F$, it is called <span style="color:#00bfff">F-intolerant</span>

To satisfy safety and liveliness, we need two program components:
- [[detectors]] - used to design fail-safe fault tolerance
- [[correctors]] - used to design non-masking fault tolerance

They are both used to design masking fault tolerance

![[Pasted image 20250130120353.png]]

### Phases of Fault Tolerance

![[Pasted image 20250130120515.png]]

Error detection is achieved by detector components
Error recovery is achieved by corrector components

Damage assessment is investigating how far error has propagated
- how many modules were affected

Fault treatment is usually done offline to rectify problems

### Recovering from Errors
#### Forward error recovery
Upon detection of an error, program attempts to get into a state which is no longer erroneous
#### Backward error recovery
Upon detection of error, program rolls back to a previously recorded good point from which it can restart executing

### Checkpointing
Checkpoints must be taken in a consistent way to avoid cascading roll-back

We need a checkpointing scheme that is generally applicable

#### Recovery Line
A recovery line is a set of checkpoints across all processes to which the programs can be rolled back in the event of failure, to ensure consistent error-free state of the system

A recovery line is said to be consistent if there are no messages that originate after the line and terminate before it
- Along the recovery line, there can not be a receive without a corresponding send
- The reverse is allowed because the receive will occur after the send

A recovery line is basically a good checkpoint

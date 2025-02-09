# N-Version Programming
NVP is defined as the independent generation and utilisation of $N$ functionally equivalent programs $\forall N \geq 2$ 

It's typically implemented with majority voting but this isn't strictly required

Characterised as $N$ hardware channels and $N$ software channels

N-Version programming uses a lot of resources so is only used in scenarios where it's needed

For NVP:
- All versions need to be synchronised
	- Results from rounds need to be compared - therefore need to be sync'ed
	- May require long wait states for synchronisation
- N hardware channels may have different properties
- If comparisons are rare, long wait times could be acceptable
### No Majority Voting
When $N = 2$, majority voting isn't possible
- logging and error detection are preferable in some applications

We can still take corrective action even with only 2 versions

A lack of agreement indicates that a problem occurred

Generally, its impossible to precisely identify the erroneous version but we have still detected an error

We have a couple options to do with only 2 versions:
- <span style="color:#00bfff">Return to start state</span>
	- Known to be safe
	- Spec can be reinforced after execution resumes
- <span style="color:#00bfff">Transition to a safe state</span>
	- Similar to restart
	- Used where infrequence 'halt' is acceptable
	- Not recommended where continuous provision of service
- <span style="color:#00bfff">Rely on designating a more reliable version</span>
	- Liveness is preserved
	- Used where liveness is more important than safety
- <span style="color:#00bfff">Diagnostic Selection</span>
	- Selection of best based on analysis of output
	- Done by a diagnostic program

### With Majority Voting
Majority voting is possible when $N \geq 3$
- often only 3

Independent programs providing identical output formats
Acceptance program that evaluates the first output requirement and selects the result for the N version output
A driver invokes the above points and provides the output to other programs or physical systems

### Assumptions in NVP
**The NVP Axiom:** 
- NVP is most efficient if version failures occur independently

NVP will not work if all versions fail on same inputs


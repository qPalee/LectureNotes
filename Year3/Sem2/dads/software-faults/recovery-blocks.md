# Recovery Blocks
![[Pasted image 20250130124442.png]]

- Recovery Blocks have one hardware channel and $N$ software components
- Secondary components perform similar function but in a different way
- Acceptance testing decides whether results are acceptable

If a primary component fails an acceptance test, we reload a checkpoint and execute a secondary from a clean state

Checkpoints are a snapshot of the system state at the point of primary execution

Recovery blocks have:
- redundancy in space (many versions) and time (executing multiple versions)
- tolerate design flaws and hardware faults
- difficult to design good acceptance checks
	- can have problems with false positives
- Needs ot accepts results from last module which could be unreliable

This is not N-version programming as there is only one hardware channel

With recovery blocks there is a balance between if you want more false positives or false negatives

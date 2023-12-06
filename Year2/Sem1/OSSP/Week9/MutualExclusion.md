# Mutual Exclusion for cooperating processes

Processes cooperate through shared memory. When multiple processes share memory data, things can go wrong very quickly.

### Challenges to Shared Memory Consistency
In a single process, your program dictates the order of execution.
When there are multiple processes, the order of execution is not guaranteed

### Critical Section Problem
When the order in which shared data is accessed matters, we say there is a <span style="color:#00bfff">race condition</span>. 

The OS kernel is full of potential race conditions, since it serves interrupts, preempts processes abd serves many processes at once

A main source of race conditions is the interleaving of processes manipulating the data

To solve this each program will have a Critical Section.
##### A protocol which solves the critical section problem should guarantee:
- <span style="color:#00bfff">Mutual Exclusion</span> - If process P is in its critical section, then no other processes can be in their critical section
- <span style="color:#00bfff">Progress</span> - No indefinite blocking
- <span style="color:#00bfff">Bounded Waiting</span> - There is a bounded time in which any process is allowed to enter its critical section

#### Locks
All solutions to the critical section problem require a lock

A process requires a lock before entering a critical section, then releases the lock after leaving the critical section

The general patter for using locks is 
```C
do
{
	[Aquire Lock]
		[Critical Section]
	[Release Lock]

	[Remainder Section]
}while(True);
```

##### A naïve locking algorithm
In these algorithms, we always write in terms of process $P_i$ and $P_j$. Doing so allows us to write the multi-party algorithms as succinct as possible.

##### Petersons Algorithm
![[Pasted image 20231120121603.png]]
When both processes are interested, they achieve fairness through the **turn** variable, which causes their access to alternate.

### Synchronisation Hardware
*some yapping*

#### TestAndSet
TestAndSet is a CPU instruction which sets a variable to TRUE then returns the original value

If it returns FALSE, we know our thread has changed the value from FALSE to TRUE
- We have the lock
If it returns TRUE, we know we haven't changed the value
- Someone else is using the lock

![[Pasted image 20231120122332.png]]

#### Spinlock
In out TestAndSet algorithm, we have a while loop which cycles constantly using CPU cycles until it manages to enter the critical section, which is known as a <span style="color:#00bfff">spinlock</span> and is a waste of CPU cycles

Instead of cycling until it proceeds, we can have a mechanism where out process sleeps and don't wake up until the lock is opened, in which the process using the lock will wake up all threads currently sleeping which are waiting for the lock so they can try again

### Semaphores
Semaphores are a synchronisation tool which:
- Simplifies synchronisation for the programmer
- Doesn't require busy waiting
- Can guarantee bounded waiting and time and progress

continue on slide 28 lad



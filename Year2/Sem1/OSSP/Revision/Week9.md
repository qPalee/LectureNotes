# Week 9
### Semaphores
Semaphores are a synchronisation tool which:
- Simplifies synchronisation
- Doesn't require much busy waiting
- Can guarantee bounded waiting time and progress

It consists of:
- A semaphore that records a list of waiting processes and an integer
- Two standard <span style="color:#00bfff">atomic</span> operations to modify `S:wait()` and `signal()`

#### How semaphores work
The semaphore in initialised with a count value of the maximum number of processes allowed in the critical section at the same time

When a process calls `wait()`, if count is zero it adds itself to the list of sleepers, else it decrements and enters the critical section

When a process exits the critical section it calls `signal()`, which increments count and issues a wakeup call to the process at the head of the list


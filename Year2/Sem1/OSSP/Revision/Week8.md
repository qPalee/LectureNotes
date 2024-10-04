# Week 8
### Processes
A process is a program in execution and includes:
- program (text) and program counter
- stack
- data section
- heap

#### Process States
Processes have many different states and as it executes it will change state
- <span style="color:#00bfff">new</span>: the process is being created
- <span style="color:#00bfff">running</span>: instructions are being executed
- <span style="color:#00bfff">waiting</span>: the process is waiting for an event to occur
- <span style="color:#00bfff">ready</span>: the process is waiting to be assigned to a processor
- <span style="color:#00bfff">terminated</span>: the process has finished execution

#### Process Control Block
Information associated with each process, which is stored as various fields within a kernel data structure
- Process state
- Program Counter
- CPU registers
- CPU scheduling information
- Memory management information
- Accounting information
- I/O status information
#### Process Creation
Parent processes create child processes, which then can make processes themselves
This forms a tree of processes

In general, processes are identified and managed via a process identifier (pid)

##### Resource Sharing
When a parent makes a child, they can choose what to share with them
- Share all resources
- Children share a subset of parents resources
- Share no resources

During execution parent and child processes execute concurrently
The parent will wait until their children all terminate

#### Process Termination
To terminate, a process must execute its last statement then ask the OS to delete it (exit state)
- Data is output from child to parent (via wait)
- Processes resources are deallocated by OS

A process' parent may terminate execution instead
This can happen if:
- Child has exceeded allocated resources
- Task assigned is no longer required

### Scheduling
Scheduling is needed because in an OS there are many processes competing for resources

#### Scheduling algorithms
##### First Come First Served
Jobs are put in a queue and served according to arrival time

Easy to implement but CPU intensive processes can cause long wait times

Must get the time before preemption right:
- <span style="color:#00bfff">too short</span>: too many context switches
- <span style="color:#00bfff">too long</span>: process can monopolise cpu

##### Shortest Job First
Scheduler chooses the job with the <span style="color:#00bfff">shortest CPU burst time</span>

This is not implementable, but is the algorithm with the smallest average waiting time

##### Priority Scheduling
For priority Scheduling to work, each process much have an associated priority

CPU is allocated to the process with the highest priority
Equal priority processes are scheduled according to first come first served

There are two variations of this:
- <span style="color:#00bfff">With preemption</span>: newly arrived process with higher priority gains processor immediately form lower priority process
- <span style="color:#00bfff">Without preemption</span>: newly arrived process must wait for currently running process to finish

Preemption is good for ensuring a quick response time for high priority processes

<span style="color:#ff0000">Starvation of low priority processes is possible</span>
- Fix this by increasing priority of processes after a while
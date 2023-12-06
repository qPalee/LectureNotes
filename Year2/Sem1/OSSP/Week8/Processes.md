# Processes
A process if a program in execution
execution must progress in sequential fashion

### Process Control Block
Information associated with each process, which are stored within a kernel data structure
- Process state
- Program Counter
- CPU registers
- CPU scheduling information
- Memory-management information
- Accounting information
- I/O status information

#### Process Creation
Parent processes create children, which in turn create other processes, forming a tree
Generally, process managed via <span style="color:#00bfff">process identifier (PID)</span> 

##### Resource sharing
- Parent + child share resources
- Children share subset of parent's resources
- Parent + child share no resources

##### Execution
- Parent + children execute concurrently
- Parent waits until children terminate

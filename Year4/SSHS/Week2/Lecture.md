# Lecture

### File Descriptors
- UNIX has 2 system calls `dup()` and `dup2()`

#### dup
- `int dup(int filedes)`
- Duplicates specified file descriptor and returns a new unused one
- Internal file struct isn't duplicated, only the pointer to it

#### dup2
- `int dup2(int filedes1, int filedes2)`

### Sandboxing

#### Modern Linux sandboxing
`seccomp` enables a process to lock itself out of 

It starts up processes then the child invokes `seccomp` to give up and privileges it got from its parent

### Process Communication
Done in two ways
- Standard Unix pipes/file descriptors
	- Basically a network program
- Shared memory
	- Need to be much more careful

### Virtual Machines
Use cases:
- Isolation and Sandboxing
- Resource Allocation
- System Management
- Cross-platform testing

### Hypervisors
There are two types of hypervisor: <span style="color:#00bfff">bare metal</span> and <span style="color:#00bfff">hosted</span>

## Docker

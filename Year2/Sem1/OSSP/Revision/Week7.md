# Week 7
### Memory Management
Memory is a limited resource
Complex algorithms are needed, together with support from hardware and compiler

A programs view of memory is a set of memory cells starting at 0x0 and finishing at some value
A program accesses <span style="color:#00bfff">logical addresses</span>

Hardware has a set of memory cells starting at 0x0 and finishing at some value, but they are <span style="color:#00bfff">physical addresses</span>

We want to be able to store memory of several programs in main memory at the same time
For this we need suitable mapping from logical addresses to physical addresses

This is done a couple ways:
- at <span style="color:#00bfff">compile time</span>: absolute references are generated
- at <span style="color:#00bfff">load time</span>: can be done by special program
- at <span style="color:#00bfff">execution time</span>: needs hardware support

#### Swapping
If memory usage is too high, some processes' memory is transferred to disk

Usually combined with scheduling to ensure low priority processes are swapped out first

Problems:
- Long transfer time
- What to do with pending I/O?

##### Fragmentation
Over time swapping causes fragmentation
- Many small holes appear in memory

Strategies for choosing holes:
- <span style="color:#00bfff">First-fit</span>: Start from beginning and use first available hole
- <span style="color:#00bfff">Rotating first fit</span>: Start after last assigned part of memory
- <span style="color:#00bfff">Best fit</span>: find smallest usable space
- <span style="color:#00bfff">Buddy System</span>: Have holes in sizes of power of 2 and use smallest possible hole

##### Paging
Paging is done by assigning memory of a fixed size
- Avoids <span style="color:#00fc00">external fragmentation</span>

Translation of logical addresses to physical addresses done via page table

Hardware support is mandatory for paging
- If page table is small, use fast registers
- Store large page tables in main memory but cache most recently used entries

![[Pasted image 20240515135649.png]]

#### Segmentation
Divide memory according to its usage by programs:
- <span style="color:#00bfff">Data</span>: <span style="color:#00fc00">mutable, different</span> for each instance
- <span style="color:#00bfff">Program Code</span>: <span style="color:#00fc00">immutable, same</span> for each instance
- <span style="color:#00bfff">Symbol Table</span>: <span style="color:#00fc00">immutable, same</span> for each instance, <span style="color:#ff0000">only necessary for debugging</span>

Also requires hardware support

Paging is motivated by ease of allocation whereas segmentation is motivated by use of memory
- A combination of the two works well

### Virtual Memory
Complete separation of logical and physical memory
- Program can have an extremely large amount of virtual memory

This works because most programs will only use a small fraction of memory intensively

It is very tricky to implement efficiently due to the speed difference between ram and disk

### Memory in the Linux Kernel
The kernel only has four segments in total:
- Kernel Code
- Kernel Data
- User Code
- User Data

Paging is used with an elaborate permission system for pages

There are separate logical addresses for kernel and user memory
For 32-bit systems:
- kernel space addresses are the upper 1GB of addresses ($\geq \text{0xC0000000}$)
- user space addresses are the lower 3GB of addresses ($\leq \text{0xBFFFFFFF}$)

For 64-bit systems:
- kernel space addresses are the upper half of addresses ($\geq \text{0x8000 0000 0000 0000}$)
- user space addresses are the lower half of addresses ($\leq \text{0x7FFF FFFF FFFF FFFF}$)

Kernel memory is always mapped but is protected against access by user processes

### Kernel Programming

#### Very simplified structure of kernel
```
initialise data structures at boot time;
while (1)
{
	while (timer not gone off)
	{
		assign CPU to suitable process;
		execute process;
	}
	
	select next suitable process;
}
```

#### Interaction between kernel and user programs
Kernel provides its functions only via system calls

There is a very strict separation of kernel data and user data
Need to have explicit copying between user program and kernel

##### Data transfer
- Linux maintains a dir called `proc` as an interface between user space and kernel
- Files in this directory do not exist on disk
- RW operations on these files are translated into kernel operations
- Useful for information exchange between user and kernel space

#### Kernel modes
The structure of the kernel gives rise to two main modes for kernel code:
- <span style="color:#00bfff">process context</span>: kernel code working for user programs by executing a system call
- <span style="color:#00bfff">interrupt context</span>: kernel code handling an interrupt

- The kernel only has access to user data in process context
- Any code running in process context may be pre-empted by an interrupt
- Interrupts have priority levels
- Interrupts of lower priority are pre-empted by interrupts of higher priority



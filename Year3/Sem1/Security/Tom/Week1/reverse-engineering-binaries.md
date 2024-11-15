# Reverse Engineering Binaries
### x86-64 architecture
![[Pasted image 20240930152513.png]]
RAX is a big 64 bit working space
RIP points to the next instruction to run
RSP and RBP are the stack pointers

If the stack ever hits the heap the program crashes due to lack of memory
#### Subparts of registers
![[Pasted image 20240930153043.png]]
These are different ways of reading the same register

We were lied to last year
Functions are called differently
- The first 6 args are called with registers and the rest is on the stack

#### Functions
##### Linux
Arguments are put in registers
- RDI, RSI, RDX, RCX, R8, R9 and then they are put onto the stack
- XMM0, XMM1, ... , XMM7 for floating point numbers
Results return in RAX and RDX or XMM0 and XMM1

The function makes a new stack space by moving the stack pointers (RSP, RBP)
Instruction pointers and old RBP are stored on the stack for later

##### Windows
Windows uses different registers
- RCX, RDX, R8, R9 or XMM0, XMM1, XMM2, XMM3

After a function finishes the old RBP and RIP are restored so the program can continue running
The return function goes into the RAX register (which is why C programs must return a pointer)

![[Pasted image 20241002183220.png]]
This is the dumbest thing ever
I was happier not knowing this information
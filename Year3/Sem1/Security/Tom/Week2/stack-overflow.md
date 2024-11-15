# Buffer Overflows
The Instruction Pointer (RIP) controls which code executes

The instruction pointer is stored on the stack
We can write to the stack
- We can overwrite the instruction pointer

ARM has the same problem as x64 but it just needs a layer of redirection

### NX-Bit
No memory is both writeable and executable
It will only be one or the other

### Address space layout randomisation
ASLR adds a random offset to the stack and codes base each time the program runs
Jumps in the program are altered to point to the right line
The idea is that its now hard for an attacker to guess the address of where they inject code or the address of particular functions

### Stack Canaries
At the start of a function a random value from the heap is written to the base of the stack
When the function finishes the value on the stack is checked against the value on the heap
If the values aren't the same it will be flagged
In Windows, the stack canary is xor-ed with the RBP to make a different value for every function
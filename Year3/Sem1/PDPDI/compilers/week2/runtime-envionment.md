# Runtime environment
A compiler must correctly map the high-level constructs of the source language to the low-level target machine constructs.
To do so it makes use of a runtime environment, which is a collection of data structures maintained at runtime

### Storage Optimisations
The target code runs in its own logical address space
The kernel maps the logical addresses into physical addresses
The virtual memory is divided into two areas
- program code
- data

- The target code is compiled and stored in code (.text)
- Some objects are fixed at compile time and stored in static (also .text)
- The stack stores activation records generated during procedure calls, and starts from a high address and grows downwards (mov ebp, ebp - stack_frame)
- The heap stores dynamically allocated data and starts from a lower address and grows upwards

A storage unit is a byte
The runtime storage comes in blocks of continuous bytes

Variables are assigned types during type checking, from which can be derived the amount of memory it requires to be stored

Objects that use multiple bytes are stored in consecutive bytes and assigned the address of the first byte


### Activation Records
The stack is devided into blocks, called activation records, or stack frames, which are
- pushed onto the stack every time a function is called
- popped when the function returns

It hold local vars, parameters, return address and other temp values

A stack pointer identifies where the current stack frame is on the stack (rbp/ebp)

The calls of procedures can be organised in an activation tree, showing the calls in the order they happen

Recursive functions create a lot of stack frames which eats through a lot of memory
![[Pasted image 20241122153136.png]]
![[Pasted image 20241122153919.png]]


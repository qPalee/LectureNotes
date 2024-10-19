# Advanced Memory Attacks

### NX-bit - W xor X
Executable code should be on the text section of memory, not the stack
The NX bit provides a hardware distinction between the text and the stack
When enabled, the program will crash if the RIP ever points to the stack

#### Bypass
We can bypass this by using reusing code from the executable section of memory
This could be functions from the main library or any loaded library
We can jump to any point in a function, not just the start

We can queue up instruction pointers on the stack and execute them one after another

#### Return to libc
The standard C library <span style="color:#00bfff">libc</span> is almost always loaded
This function has many useful functions we could call
- There is a 'system' function which will run any command

The memory map will tell you where it is loaded
- `/proc/<process ID>/maps` for running linux processes

Function offsets can be found in IDA and many other tools

64 bit is a bit harder since arguments go into registers first
You can initially return to a function which pops rdi and puts it onto the stack

### Integer Overflow
`int` doesn't behave like numbers in maths
We can control ints and exploit the system

### Memory Allocation Vulnerabilities
Incorrect memory allocation can lead to vulnerabilities

#### Use after free
`malloc -> use -> free -> use`
After the free() the data remains in memory so the program may work
However other data could be allocated in its place
If the attacker controls the new data they also control the old data

### Format String Vulnerabilities
`printf` in C is very weird
There is no check that the number of `%` in the string matches the number of arguments

What happens if you try to do `printf("%p");`?
The code will reach `%p` and try to look for the argument

The first argument `"%p"` will be in the RDI register (RCX on windows) so the code will look into the RSI register (RDX on windows) and print whatever is there

`printf(%p %p %p %p %p %p %p %p);` will print RSI, RDX, RCX, R8, R9 and the top three values on the stack

If the attackers can control the string being printed, then they can look on the stack to find addresses, and the stack canary
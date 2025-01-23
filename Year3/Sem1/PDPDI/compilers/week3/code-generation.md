# Code Generation
Compilers generate a target program from the intermediate representation

Generating an optimal program is undecidable

Compiler builders rely on heuristics
To generate efficient target code, compilers rely on optimisations

A code generator performs:
- Instruction selection
- Register allocation
- Instruction ordering

### Instruction Selection
Translating high-level IR is easy
Making it efficient is hard
![[Pasted image 20241125121015.png]]
With a simple program it is easy to make efficient

![[Pasted image 20241125121043.png]]
With more complex programs, it's harder to optimise
There is no need to load a into R0 since its already there
We are doing an extra instruction for no reason

#### Target Language
We will consider:
- a simple assembly language
- a three-address machine
- byte-addressable machine
- n general-purpose registers

##### Instructions
- <span style="color:#00bfff">LD dst, addr</span>: loads the value at the address <span style="color:#00bfff">addr</span> into the location <span style="color:#00bfff">dst</span>
- <span style="color:#00bfff">ST dst, r</span>: stores the value in register <span style="color:#00bfff">r</span> into the location <span style="color:#00bfff">dst</span>

##### Addressing modes
A location can be:
- a variable name $\textcolor{#00bfff}{x}$, referring to the memory location reserved for $\textcolor{#00bfff}{x}$
- an indexed address of the form $\textcolor{#00bfff}{a(r)}$, where $\textcolor{#00bfff}{a}$ is a variable and $\textcolor{#00bfff}{r}$ is a register: adds the value in register $\textcolor{#00bfff}{r}$ to $\textcolor{#00bfff}{a}$
- an interger indexed by a register of the form $\textcolor{#00bfff}{n(r)}$

Indirect addressing modes:
- $\textcolor{#00bfff}{* r}$:
- $\textcolor{#00bfff}{*n(r)}$:


##### Arithmetic
The TAC $\textcolor{#00bfff}{x=y-z}$ can be translated into:
- LD R1, y
- LD R2, z
- SUB R1. R1, R2
- ST x, R1

It may be possible to omit some instructions, such as if y is already a register

##### Jumps
The statement $\textcolor{#00bfff}{if \ x < y \ goto \ L}$ can be translated into:
- LD R1, x
- LD R2, y
- SUB R1, R1, R2
- BLTZ R1, L

where L is the label that represents the 1st machine instruction generated from the TAC instruction named L

##### Pointers
The statements $\textcolor{#00bfff}{x = *p}$ and $\textcolor{#00bfff}{*p = y}$ can be translated into:
- LD R1, p
- LD R2, 0(R1)
- ST x, R2

- LD R1, p
- LD R2, y
- ST 0(R1), R2

##### Arrays
Dont need to know this but nice to know

Let $\textcolor{#00bfff}{a}$ be an array of 8-byte elements: The TACs $\textcolor{#00bfff}{b = a[i]}$ and $\textcolor{#00bfff}{a[j] = c}$ can be translated into
- LD R1, i
- MUL R1, R1, 8
- LD R2, a(R1)
- ST b, R2

- LD R1, c
- RL R2, j
- MUL R2, R2 8
- ST a(R2), R1

##### Generating Target Code
Generate target code for:
- x = a \* b
- y = x + c

This will translate into
- LD R1, a
- LD R2, b
- MUL R1, R1, R2
- ST x, R1
- LD R2, c
- ADD R1, R1, R2
- ST y, R1

#### Instruction Costs
A simple cost function:
- all instructions have a default cost of 1
- accessing a register has a cost of 0
- accessing a memory location or a constant has a cost of 1

##### Examples:
- LD R0, R1 has a cost of 1
- LD R0, M has a cost of 2
	- where M hold the content of a memory location

Cost of $\textcolor{#00bfff}{LD \ R1, *100(R2)}$: 3
Cost of $\textcolor{#00bfff}{x=y+z}$: 7

#### Procedures
When q calls p:
- control needs to be given to p
- once p is done, control needs to return to q

p returns by calling `return y;` or `return`

When q calls p, it stores its return address in the generated activation record for p. Assume for simplicity that it is the first component of this activation record. The target code can be:
- <span style="color:#00bfff">ST p.staticArea, #next</span>
- <span style="color:#00bfff">BR p.codeArea</span>

where:
- <span style="color:#00bfff">p.staticArea</span> is the address of the beginning of p's activation record where the return address is stored
- <span style="color:#00bfff">#next</span> is the return address
- <span style="color:#00bfff">p.codeArea</span> refers to the address of p's first instruction in the code area

When p returns, control is given back to q by jumping to the return address (<span style="color:#00bfff">BR *p.staticArea</span>)

<span style="color:#00bfff">p.staticArea</span> can be implemented by a register PS that stores the address of the current stack frame

A procedure call with this looks like:
- <span style="color:#00bfff">ADD SP, SP, #caller.recordSize</span>
- <span style="color:#00bfff">ST *SP, #next</span>
- <span style="color:#00bfff">BR callee.codeArea</span>
- <span style="color:#00bfff">SUB SP, SP, #caller.recordSize</span>

To return from a procedure, we use <span style="color:#00bfff">BR *0(SP)</span>

##### Example
![[Pasted image 20241125132616.png]]

### Basic Blocks
Basic Blocks are used to help with instruction selection. They form the nodes of flow graphs which are used to generate more optimised intermediate code

A basic block is a sequence on three-address instructions such that:
- There are no jumps into the middle of the block
- No instruction in the block halts or branches, except the last one

#### Partitioning Algorithm
Given a sequence of three-address blocks:
- Identify the leaders
	- The first instruction in the sequence
	- Any instruction which is the target of a conditional jump
	- Any instruction which immediately follows a conditional jump
- A basic block consists of a leader, plus all the following instructions up to the next leader

##### Example
![[Pasted image 20241125132936.png]]

#### Flow Graphs
A flow graph has
- basic blocks as nodes
- edges that capture the control flow between blocks

There is an edge from block $B_1$ to $B_2$ if and only if
- there is a conditional jump from the end of $B_1$ to the beginning of $B_2$
- or $B_2$ immediately follows $B_1$ in the original sequence, and $B_1$ does not end in an unconditional jump

![[Pasted image 20241125133415.png]]

### Code Generation
Uses of registers:
- some instructions require some or all of the operands to be in registers
- temporaries
- sharing between blocks
- run-time storage management (storing stack pointer, ebp)

The generation algorithm maintains the following key data structures
- <span style="color:#00bfff">a register descriptor</span>: keeps track of the variables that currently have their values in registers
- <span style="color:#00bfff">an address descriptor</span>: keeps track of the locations where the current values of variables are stored

We will assume a`getRegI)` function, which given an instruction `I`, returns a register for each memory location associated with `I`. We will see later how to implement it

#### Algorithm for operations
Given an instruction `I` of the form $x=y+z$
- use `getReg(I)` to select registers: $R_x, R_y, R_z$ for $x, y, z$
- if $y$ is not in $R_y$, then generate $\textcolor{#00bfff}{LD \ R_y, \ y'}$ where $y'$ is one of the memory locations for $y$
- do the same for $z$
- generate $\textcolor{#00bfff}{ADD \ R_X, \ R_y, \ R_z}$

#### Algorithm for copy
Given an instruction `I` of the form $x=y$
- we assume that `getReg(I)` returns a single register $R$
- if $y$ is not already in $R$, generate $\textcolor{#00bfff}{LD \ R, \ y}$
- if $y$ is in $R$, do nothing

#### Updating descriptors
The register and address descriptors can be updated as follows:

For the instruction <span style="color:#00bfff">LD R, x</span>
- register descriptor: <span style="color:#00bfff">R</span> holds <span style="color:#00bfff">x</span> only
- address descriptor: <span style="color:#00bfff">R</span> is a location for <span style="color:#00bfff">x</span>

For the instruction <span style="color:#00bfff">ST x, R</span>
- address descriptor: <span style="color:#00bfff">x</span> is a location for itself

For the instruction $\textcolor{#00bfff}{ADD \ R_x, \ R_y, \ R_z}$
- register descriptor: $\textcolor{#00bfff}{R_x}$ holds $\textcolor{#00bfff}{x}$ only, and only $\textcolor{#00bfff}{R_x}$ holds $\textcolor{#00bfff}{x}$
- address descriptor: $\textcolor{#00bfff}{x}$'s only location is $\textcolor{#00bfff}{R_x}$
- address descriptor: remove $\textcolor{#00bfff}{R_x}$ from the records of all variables other than $\textcolor{#00bfff}{x}$

![[Pasted image 20241128161241.png]]


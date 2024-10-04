# ARM

ARM uses fewer commands and therefore less power usage compared to x86

### Differences between ARM and x86
- Similar stack layout
- Smaller instruction set
- All commands are 32-bit
- Only load and store commands can read/write
- More registers - less memory access required
- Functions manage the stack themselves
- The first 7 arguments are X0-X7
- Function result is in X0

![[Pasted image 20241003134208.png]]

X addresses the entire register, W addresses the the first 32 bits
wrz is a register which always holds 0

#### Branches
Instead og jumps, ARM uses branches
Branch: b
Branch to link: bl - used to call functions

##### Conditional Branches
cmp x1 x2
bz label ; branch if zero

sub x3 x1 x2 ; x3 = x1-x2
cbz x3 label ; if x3 == 0

#### Calling Convention
- Function args go in X0 to X7
	- Optional args are always on the stack
- Function is called with `bl <function_name>`
	- Stored the pc in the lr register
- Return with ret

##### Leaf functions don't need to save the LR
It doesn't need to use memory at all but compiler is big dumb dumb


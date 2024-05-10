# The Stack (x86)
The stack grows from the highest address to the lowest address


<span style="color:#00fc00">Top of the stack = esp</span>

##### Push to the stack
When we want to push something to the stack we must <span style="color:#00bfff">push eax</span>
We must also increment the stack pointer, <span style="color:#00bfff">esp</span> (which goes down for x86)

##### Pop from the stack
When we pop from the stack, the top item is removed, and the value is added to <span style="color:#00bfff">eax</span>
After popping a value, <span style="color:#00bfff">esp</span> is decremented (which goes up for x86)

When values are popped from the stack, the data isn't actually removed from memory, it is just removed from the stack

### Functions in the stack
When a function is initialised, it creates an <span style="color:#00bfff">ebp</span>, which is the base pointer of the function

The base pointer always points to the first item on the stack that belongs to the current function, which often stores the old <span style="color:#00bfff">ebp</span>, so that it can return to it after the function is finished running





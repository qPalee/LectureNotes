# Makefile
When compiling a C program, there are 2 types of files

`<file>.c` - source code
This contains the source code for the program

`<file>.h` - include files
These files contain the function declarations of the libraries which are used by the program

`<file>.o` - Object files
These files contain assembly code for all the functions defined in `<file>.c`
They are produced by the compiler from the source code files

`<file>.so` - Shared lib files
These files contain assembly code which is suitable for inclusion in several programs

### Conventions for Makefiles
$(NAME) uses the variable NAME
The value of a variable is set with `<VariableName>=<value>`

A rule has the form:
```Makefile
<target>: <file1> ... <filen>
	<command>
```
If file target does not exist or any of `file1. . .filen` are newer than target, then 'command' is executed

#### Special variables
`$@` means target
`$<` means file1
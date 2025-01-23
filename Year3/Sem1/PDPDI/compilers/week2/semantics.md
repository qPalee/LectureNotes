# Semantics

### Problem
- <span style="color:#00bfff">Lexer</span> detects illegal tokens
- <span style="color:#00bfff">Parser</span> detect whether input is part of the language
- <span style="color:#00bfff">Semantic analysis</span>
	- Checks the semantics oof the program
	- variables are declared, expressions have correct type

#### Example 
![[Pasted image 20241118121813.png]]

### Semantic Actions
The parsers we discussed so far do not do anything useful with the sentences
They can be extended with semantic actions

<span style="color:#00bfff">We indicate semantic actions using curly braces</span>

We can write an interpreter with this
![[Pasted image 20241118122155.png]]

Note:
- The rules all return a number
- E() returns the value returned by the semantic action called when parsing E, and similarly for other non-terminal symbols

wallahi i need to rewatch this lecture later
18/11/24

$\textcolor{#ff0000}{x:=2 ; y:=x+1}$
- $\textcolor{#00ff00}{\{x \rightarrow 2, y \rightarrow 3\}}$
$\textcolor{#ff0000}{[x:=2] ; y:=x+1}$
- <span style="color:#00fc00">looking up</span> $\textcolor{#00fc00}{x}$ <span style="color:#00fc00">fails</span>
$\textcolor{#ff0000}{[x:=2 ; y:=x+1]}$
- <span style="color:#00fc00">The lookup table {}</span>

#### Abstract Syntax Tree
We could write the entire compiler as semantic actions
- This would be hard to read and maintain
- Also constraints compiler to analyze the program in the order it is parsed

Its better to seperate syntax (parsing) and semantics (type checking + translation to machine code)

Semantic actions can store the parse tree in a data structure
However, this is inconvenient to use
- useless punctuation symbols
- Too tied to the grammar, which can contain extra non-terminal symbols

Instead of this, we generate an AST

![[Pasted image 20241118123747.png]]

The BNF is ambiguous but we don't care

![[Pasted image 20241119110950.png]]

Later phases can be achieved through recursive AST walks

How do you relate errors to the source code?
- In a one-pass compiler, errors are reported using the position info provided by the lexer
- In a compiler relying on an intermediate language, the position info must be stored, often in the AST itself

This allows the type checker to produce useful error messages

### Symbol Table
This is the semantic analysis phase
- connects variable definitions to their uses
- checks that expressions are well-typed

Some of this info is maintained in a symbol table, which maps identifiers to their types and locations

Identifiers are inserted into the symbol table when declared
They are then looked up in the symbol table when used

Symbol tables can by implemented in
- <span style="color:#00fc00">an imperative style</span>
- <span style="color:#ff0000">a functional style</span>

We won't be looking at the functional style

##### Imperative Style
Implemented as a hash table with linked lists for all elements which hash to the same bucket
Linked list may contain types to be used for type-checking

![[Pasted image 20241119112440.png]]

im so fucking cooked
- im not as cooked anymore

#### Type checking
A similar approach can be used to type check programs

Type checking is used to:
- catch semantic errors
- determine the number of storage units needed for the variables of the program

Those storage units are used to compute at compile time, relative addresses where variables will be stored
- variables are stored in the same place relative to the start of the program
- they end up being in different places each time due to ASLR
- pointer paths :)


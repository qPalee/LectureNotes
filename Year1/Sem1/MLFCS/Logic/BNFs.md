<h1>BNF's</h1>

lhs ::= rhs1 |...| rhs2
The lhs can expand to any of the forms on the rhs
Each rhs is a sequence of non terminal and terminal symbols

**Example:**
exp ::= num | exp + exp | exp x exp
ehere a numeral num is a sequence of digits. Here exp is a non-terminal symbol and +, x, ,0, 1 etc... are terminal symbols

Arity + fixity
- 0, 1 are nullary (arity 0) operators (constants)
+ + and x are binary (arity 2) infix operators

Conditional Operators
On rhs, **if** *b* **then** *exp* **else** *exp*
 
BNF for propositional logic

P ::= a | P -> P | P OR P | P AND P | NOT P
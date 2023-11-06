Semantics assigns meanings/interpretations with fornulae

The basic notation used is **"truth value"**

The 2 standard truth values are true and false (T, F)

Truth Assignment
- Function assigning a truth value for each atomic proposition
- Given 2 atomic propositions *p, q*, if the formula is $p \lor q$
- then one truth assignment $\phi$ is $\phi (p) = T$ and $\phi (q) = F$
- Also called an**interpretation**or a **valuation**

4 truth valuations are needed to be considered for $p \lor q$, because $2^2 = 4$ 

**Conventions**
The atoms $\top , \bot$ have the interpretations T, F respectively

### Extending notation of semantics to **compound formulas**

Define semantics for the 4 logical connectives: $\lor , \land , \rightarrow , \lnot$
This is done **recursively bottom-up** over the structure of propositions

## Extended valuation function
*Get off slides, too much writing rn*

What is $\phi (2 \geq 1 \land 1 \geq 0)$?

$\phi (2 > 1 \land 1 > 0) = \top \text{ because } \phi (2 > 1) = \top \text{ and } \phi (1 > 0) = \top$

## Satisfiability and Validity
The above technique allows answering of the following question
What is the truth value of a formula with respect to a given valuation of its atoms

Given a valuation $\phi$ on all atomic propositions, we say that $\phi$ satisfies A is $\phi (A) = \top$
A is satisfyable if there exists a valuation $\phi$  such that $\phi(A) = \top$ 
A is valid ...

### Truth tables
They still exist :(, havent changes at all
If you forgot them youre a silly cunt

Implies now exists but its bare easy, for *A, B* $A \implies B \iff B = \top \text{ whenever } A = \top$ 
If $A = \bot$, $A \implies B = \top$

- A formula is **satisfiable** iff there is a valuation that satisfies it -> $\top$ in rightmost column
	Example: $p \land q, \text{ where } \phi(p) = \top \text{ and } \phi(q) = \top$
- A formula is **falsifiable** iff here is a valuation that makes it false -> $\bot$ in rightmost column
	Example $p \land q, \text{ where } \phi(p) = \top \text{ and } \phi(q) = \bot$
- A formula is **unsatisfiable** iff no valuation satisfies it -> all $\bot$ is rightmost column
	Example $p \land \lnot p$ (contradiction)
- A formula is **valid** iff every valuation satisfies it -> all $\top$ in rightmost coloum
	Example $p \lor \lnot p$ (tautology

### Validity
- **Syntactically** - we can derive the conclusion from the premises
- **Semantically** - the conclusion is true whenever the premises are true

If a formula is provable in **Natural Deduction**, then it is semantically valid, and vice versa

Formally, we write 
$$P_1 .......P_n \models C$$
Checking $P_1 .......P_n \models C$ is the same as checking the validity of $P_1 \implies .......P_n \implies C$
-> The cells on the rightmost column of $P_1 \implies .......P_n \implies C$ all contain $\top$

Check iff whenever all premises are true, then the conclusion is true. If this is the case then its valid (sheesh)

## Soundness and completeness
A deduction system is sound with respect to a semantic if every provable formula is valid
- $\text{If } \vdash A \text{ then } \models A$

A deduction system is complete with respect to a semantic if every valid formula is provable
- $\text{If } \models A \text{ then } \vdash A$


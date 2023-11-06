A proof of $A \land B$ can be viewed as a **pair** of a proof of A and a proof of B
A proof of $A \implies B$ can be viewed as a **procedure** which trabsforms evidence for A into evidence for B
A proof of $A \lor B$ is either a proof of A or a proof of B, which indicated which one it is
Classical proofs rely on Boolean truth tables
They also introduce additional reasoning principles

Proof by contradicion is a typical classical reasoning tcehnique
- If $\lnot A \implies \bot$ then A
- That is $\lnot \lnot A \implies A$

Law of excluded Middle (LEM)
For each A we can always prove one of A or $\lnot$ A

Double Negation Elimination (DNE)
$\lnot \lnot A \implies A$

As rules:
$$\frac{}{A \lor \lnot A}[LEM]$$
$$\frac{\lnot \lnot A}{A}[DNE]$$

## Contrapositive
Given an implication $A \implies B$, the formula $\lnot A \implies \lnot B$  is called the **contrapositive**.



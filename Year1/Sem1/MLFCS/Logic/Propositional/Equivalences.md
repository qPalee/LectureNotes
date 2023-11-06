Let $A \Leftrightarrow B$ be defined as $(A \implies B) \land (B \implies A)$
- This means that A and B are logically equivalent
- A and B have the same semantics
- $\phi(A) = \top \iff \phi(B) = \top$
- ...

Equivalences can be used to replace a premise with another one that is easier to work with

Some examples of equivalences:
- De Morgan's Law (I)
$$\lnot(A \lor B) \Leftrightarrow (\lnot A \land \lnot B)$$
- De Morgan's Law (II)
$$\lnot(A \land B) \Leftrightarrow (\lnot A \lor \lnot B)$$
- Implication emimination
$$(A \implies B) \Leftrightarrow (\lnot A \lor B)$$

### How to prove logical equivalences
You can treat it like an and equation
$$\frac{\frac{B}{A \implies B}1[\rightarrow I]\frac{A}{B \implies A}2[\rightarrow I]}{A \leftrightarrow B}[\land I]$$
Or you can prove both left-to-right and right-to-left implication
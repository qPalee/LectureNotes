Inference rules are the tools that we are allowed to use

Notation:
- Premises at the top
- Conclusion at the bottom
- Name to the right
 

False-elimination
$$\frac{\bot}{A}[\bot E]$$

True-introduction
$$\frac{}{\top}[\top I]$$
Implication-introduction
$$\frac{B}{A \rightarrow B}[\rightarrow I]$$Implication-elimination
$$\frac{A \rightarrow B \space \space \space A}{B}[\rightarrow E]$$
Negation-introduction
$$\frac{\bot}{\lnot A}1[\lnot I]$$
Negation-elimination
$$\frac{A \space \space \space \lnot A}{\bot}[\lnot E]$$
or-introduction
$$\frac{A}{A \lor B}[\lor I_L]$$
$$\frac{A}{B \lor A}[\lor I_R]$$
or-elimination
$$\frac{B \lor C \space \space \space B \implies A \space \space \space C \implies A}{A}[\lor E]$$
and-introduction
$$\frac{A \space \space \space B}{A \land B}[\land I]$$
and-elimination
$$\frac{A \land B}{B}[\land E_R]$$
$$\frac{A \land B}{A}[\land E_L]$$

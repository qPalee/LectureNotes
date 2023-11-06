Given a CNF formula, can we set $\top$ or $\bot$ value to each variable to satisfy the formula?

Example: 
Consider the formula $(A \lor \lnot B) \land (C \lor B)$
It is satisfiable by setting $A = \top$, $B = \bot$, $C = \top$
This is known as CNF Satisfiability (SAT)

P: the class of problems which we can solve in polynomial time  
NP: the class of problems where we can verify a potential  
solution/answer in polynomial time

Clearly, P $\subseteq$ NP

Is P = NP?
- This is unknown
- Most people believe $P \neq NP$ 

//Not on any exams
### Hardness of NP

Definition: A problem is NP-hard if it is at least as hard as any  
problem in NP.

More precisely, a problem X is NP-hard if any problem Y $\in$ NP  
can be solved
- Using an oracle for solving X
- plus a polynomial overhead for translating from X to Y

If P $\neq$ NP then a problem being NP-hard means it cannot be  
solved in polynomial time!

CNF-Satisfiability is NP-hard

How do you show a problem X is NP-hard?
- A polytime reduction from any of the known NP-hard problems, say SAT, to X  
- That is, show how you can solve SAT using an oracle for X  
- Plus a polynomial overhead for the translation

In practice, SAT solvers are very efficient  
(NP-hardness is the worst case)

### Should we use DNF satisfiability?

Example of a DNF formula:
$(A \land \lnot B \land C) \lor (\lnot X \land Y) \lor (Z)$

Is this satisfiable?

Its trivial to check in polytime!  
- Just pick any clause, and set variables to T or F.  

Why not use DNFs then?  
- Because changing a formula from CNF to DNF can cause exponential blowup!
- 
Brute force for SAT with N variables and M clauses needs  $2^N \times N \times M$ time  
- There are 2N truth assignments  
- For each truth assignment and each clause, verify if it is satisfied in N time

Can we solve SAT faster than $2^n$?

Conjecture (Strong Exponential Time Hypothesis (SETH)):  
SAT cannot be solved in $(2 - \alpha)^n \times poly(N+M)$ time for any  
constant $\alpha > 0$

Many state-of-the-art SAT solvers are based on the  
Davis-Putman-Logemann-Loveland algorithm (DPLL)  
Basic idea (does a lot of pruning instead of brute force):  
1. **Easy** cases
	- Atom p only appears as either p or $\lnot$ p (but not both): assign truth value accordingly  
2. **Branch** on choosing a variable p and set a truth value to it
	- This choice needs to be done cleverly  
	- If p =$\top$: remove all clauses containing p and remove all literals  $\lnot p$ from clauses  
	- If p = $\bot$: remove all clauses containing $\lnot p$ and remove all literals p from clauses  
3. Keep running the above steps **until**
	- All clauses have been removed (all true): return SAT  
	- One clause is empty (one is false): backtrack in Step 2 and choose a different truth value for p; if it is not possible to backtrack, return UNSAT

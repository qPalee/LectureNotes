# P vs NP and Algorithm Design

Polynomial better than Exponential

>[!info] Definition
>- **P** is the class of problems that can be solved in polynomial time
>- **NP** is the class of problems where we can verify a potential solution in polynomial time



Standard assumption that $P \neq NP$

### Hardness for the class $NP$

Polytime reduction: We say that $Y \leq_\rho X$ if:
- The reduction takes polynomial time
- $Y$ can be solved using a black box which solves $X$

>[!info] Definition
>A problem $X$ is $NP$-hard for all problems $Y \in NP$ we have $Y \leq_\rho X$

A problem is $NP$-hard if it is <span style="color:#00bfff">at least as hard as</span> any problem in $NP$

#### Showing a problem (SUDOKU( is $NP$-hard
- Show $Z \leq_\rho SUKOKU$ for some known $NP$-hard problem $Z$
- This is sufficient because for each $X \in NP$ we know that $X \leq_\rho Z$
- By transitivity, if follows that $\forall X \in NP, X \leq_\rho SUDOKU$

To do this we need a known $NP$-hard problem.

#### The first $NP$-hard problem

>[!info] Cook-Levin Theorem
>CNF-Satisfiability (**SAT**) is $NP$-hard

A problem being $NP$-hard means it cannot be solved in polynomial time
This is because $\forall X \in NP, X \leq_\rho SAT \land SAT \in P \Rightarrow X \in P$

#### SAT $\leq_\rho$ Almost-SAT

Given a CNF formula with $N$ variables and $M$ clauses
- SAT: Can we satisfy all M clauses
- Almost SAT: Can we satisfy $M-1$ clauses


Let the instance of SAT have the variables $x_1, x_2, ..., x_n$
We want to create an instance of Almost-SAT such that:
- All clauses of SAT are satisfied $\iff$ all but one clause of Almost-SAT are satisfied


<span style="color:#ff0000">FINISH THIS LATER FROM SLIDES</span>


#### SAT $\leq_\rho$ 3-SAT

Each clause of the instance has $\leq 3$ literals

Let the instance of SAT have the variables $x_1, x_2, ..., x_n$
If a clause has $\leq 3$ literals then keep it as is
Consider a clause with 6 literals, $C = (l_1 \vee l_2 \vee l_3 \vee l_4 \vee l_5 \vee l_6)$
Add three new variables $z_1, z_2, z_3$
- Replace $C$ with AND of the following set of clauses which we will call $D$:
	- $(l_1 \vee l_2 \vee z_1) = D_1$
	- $(l_3 \vee \neg z_1 \vee z_2)$
	- $(l_4 \vee \neg z_2 \vee z_3)$
	- $(l_5 \vee l_6 \vee \neg z_3)$
- Replace $C$ with $D_1 \land D_2 \land D_3 \land D_4 = D$


Assume the truth assignment which assigns C to False
All 6 literals will be false
- $D_1: f \vee f \vee z_1$
- $D_2 : f \vee \neg z_1 \vee z_2$
- $D_3 : f \vee \neg z_2 \vee z_3$
- $D_4 : f \vee f \vee \neg z_3$

$D_1 \rightarrow z_1$ is true
$D_2 \rightarrow z_2$ must be true
$D_3 \rightarrow z_3$ must be true
$D_4 \rightarrow$ always false
$\therefore D$ is always false = C

Max length of clause is $2N$  


#### From satisfiability to graphs

Take an instance $I$ of 3-SAT with $N$ variables and $M$ clauses
- Build a graph $G$ on $3M$ vertices as follows:
	- Introduce a $\Delta$ for each clause
	- Add conflicts to ensure every variable is not both True and False

Claim: $I$ is satisfiable $\iff G$ has an independent set of size $M$

<span style="color:#ff0000">SCREENSHOT GRAPHS FROM SLIDES WHEN UPLOADED</span>

Pink lines are triangles
Red lines are conflicts

### Algorithmic Paradigms

A problem $X$ being $NP$-hard implies that we cannot have an algorithm $ALG$ for it which satisfies both:
- $ALG$ is always correct
- $ALG$ runs in polynomial time


This has lead to development of new algorithmic paradigms such as:
- Exponential Algorithms (correct)
- Approximation Algorithms (polytime)
- Randomisation Algorithms (polytime)
- Parameterised Algorithms

# Stable Matching
We want our allocation to be <span style="color:#00bfff">stable</span>
To do this we need to introduce a notion of preferences

### Stable Matching for allocations in one group
Consider the following example:
- Preferences of A are B > C > D 
- Preferences of B are C > A > D
- Preferences of C are A > B > D
- Preferences of D are A > B > C

Every matching has an unstable pair so stable matching doesn't exist in this example

### Stable Matching for allocations in two groups
Consider this example:
- Two groups, hospitals and students, both of size $n$
- Each hospital has a ranking of the $n$ students
- Each student has a ranking of the $n$ hospitals
- Assume the list of preferences are strict and complete

Not all matchings are stable
- Consider two hospitals $h_1, h_2$ and two students $s_1, s_2$
- $h_1: s_1 > s_2$ 
- $h_2 : s_1 > s_2$
- $s_1 : h_1 > h_2$
- $s_2 : h_1 > h_2$

We have two matchings:
- $h_1-s_1 \ and \ h_2-s_2$
- $h_1-s_2 \ and \ h_2-s_1$

The second one is unstable since $h_1$ is matched with $s_2$ but prefers $s_1$ and $s_1$ is matched with $h_2$ but prefers $h_1$

The $STABLE \ MATCHING$ problem asks to find a stable matching if one exists

### How fast can we solve the stable matching problem
we know that $STABLE \ MATCHING \in NP$
- Given a matching, check the $n^2$ pairs one-by-one if they are unstable or not
- if no unstable pair, then matching is stable

This takes $n!$ time which is also written as $2^{n \ log \ n}$

## Gale-Shapley algorithm
There is always a stable matching
$O(n^2)$ time algorithm to find a stable matching
- $STABLE \ MATCHING \in P$


### Running Time
Running time can clearly be shown to be $O(n^2)$ due to the fact that in total there are $n^2$ offers, and each offer takes constant time

In the hospital + student example, each hospital will at most make $n$ offers, one to each student, and since there are $n$ hospitals the total number of offers is $n \times n$= $n^2$

### Correctness
We know that
- After getting their first offer, the students always have a better offer in hand
- If a hospital if free, there is a student that they haven't made an offer to

Theoretically, suppose Gale-Shapley returned an unstable pair $h$ and $s'$
Let $(h, s)$ and $(h', s')$ be allocations done by Gale-Shapley
- Then $h$ prefers $s'$ over $s$, and $s'$ prefers h over $h'$
The last offer made by hospital $h$ was to student $s$

We need to consider if $h$ made an offer to $s'$ before making an offer to $s$
- if NO: $h$, prefers $s$ to $s'$ - Contradiction
- if YES: $h$ was rejected by $s'$ so $s'$ prefers a different hospital

### Surprising property
Gale-Shapley always returns the same stable matching

>[!info] Theorem
>Gale-Shapley always returns the matching which matches $h$ to $BEST(h)$ for each hospital $h$




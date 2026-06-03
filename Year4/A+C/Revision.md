# Things I need to look at 

### Week 1
- Definition of NP via certificates
- Polynomial time reduction from $L \rightarrow L'$
	- such that $x \in L \iff f(x) \in L'$
	- check complexity and correctness
- NP-hardness and completeness
	- $L$ is NP-hard if for $L' \in NP$, there is a polytime reduction to $L$
	- $L$ is NP-complete if $L \in NP$ and $L$ is NP-hard
- NP is closed under $\cap$, $\cup$ and polytime reductions:
	- $L \cap L' \in NP$
	- $L \cup L' \in NP$
	- If there is a polytime reduction from $L'$ to $L$ then then $L'$ is in $NP$

### Week 2
- Polynomial time algorithms are considered efficient
- Concrete examples of NP-hardness reductions (SAT to Almost-SAT, SAT to 3-SAT, 3-SAT to Independent Set, etc). 
	- Need to show both correctness and that reduction can be done in polynomial time 
- Gale-Shapley algorithm always outputs the same stable matching.
	- This also implies that a stable matching always exists for any preference list
- If a hospital and student are first choices of each other then they are matched to each other in every stable matching

### Week 3
- Theres multiple definions of greedy algorithms
- Often not optimal
- To find a counterexample you need to reverse engineer the algo to find a case where greedy doesnt make sense to use
- Two techniques to prove correctness of greedy algorithms:
	- Show correctness at each step: show your algorithm is always as good as the optimal algorithm at each step
	- Exchange argument: look at partition problem

### Week 4
- Explain what you're storing in your DP array
- Explain base cases and what the final answer that is output
- Explain the recurrenece (correctness) which is used to compute the quantity being stored at each step
- Explain how the DP array is being built up in a consistent way
	- New entry only computed using old entries
- Time complexity to calculate each entry
- Calculate running time (size of array * time taken to compute each entry)

### Week 5
Two methods to solve recurrences
- unrolling the recurrence
- verify a possible solution by substitution

#### Unrolling a recurrence
- Preferred as you dont need to guess the answer
- also finds the correct function that satisfies the given recurrence

Steps:
- Analyze the first few steps
- Identify a pattern
- Argue how many levels are there in the recursion, then sum up over all these levels to obtain the total running time

#### Verify a possible solution
Cheatsheet just dont say anything so fuck me ig

### Week 7
- CNFs are already adequate, by constructing CNFs from truth tables
- Non-uniform models compute languages by a family of programs
	- One for each input size
- Examples of non-uniform models: CNFs, DNFs, formulas, circuits
- Examples of uniform models: Turing Machines, finite-state automata, Java
- Non-uniform models may compute undecidable languages!

- Complexity measures: Size and depth of circuits.
- Circuits of depth $d$ can be translated into logically equivalent formulas of size $O(2^d)$ and depth $O(d)$
- if a circuit family is logarithmic in depth, then we get polynomial-size formulas

### Week 8
- Translating between bases yields only linear blowup in size and depth for circuits
- Every formula can be **balanced**
	- translated to a polynomially larger one that has depth logarithmic in its size
- CNFs and DNFs are already adequate, which means so are formulas and circuits
- Methods for constructing CNFs:
	- Directly from truth table
	- From DNF representation via distributivity
	- From DNF representation of the negation, via De Morgan’s laws
- Constructing circuit families from recurrences

### Week 9
Exact Exponential Time algorithms:
- via branching 
- via DP
Fixed-parameter tractable (FPT) algorithms
- Algorithms that run in $f(k) \cdot n^{O(1)}$ time where $k$ is a parameter and $n$ is the input size

# Representing Data
For the purposes of computation, we shall identify data structures as binary strings, i.e. elements of $\{ 0, 1 \}^*$
- A natural number $\mathbb{N}$ is identified with its binary representation
- A subset $X \subseteq \{ 0, 1, ...., n-1 \}$ is identified with an $n$-bit binary string $X_0, X_1, ..., X_{n-1}$ with $X_i = 1$ iff $i \in X$
- A graph is identified with its set of edges
- A string over a finite alphabet $\Sigma$ is identified with a binary string by fixing some prefix-free coding of $\Sigma$ within $\{0, 1\}^*$

For $x \in \{0, 1\}^*$ we shall identify its length as $|x|$ and extend this notation for other data structures

### Examples

Suppose we have a set $X \subseteq \{ 0, 1, 2, 3 \}$
- $\{ 0 \} : 1000$
- $\{ 1, 3 \} : 0101$
- $\emptyset : 0000$
- $\{ 0, 1, 2, 3 \} : 1111$

# Problems
Since we define all data as binary strings, we can define:

>[!info] Definition
>A **language** or **predicate** is just a subset of $\{ 0, 1 \}^*$

We sometimes speak of a problem, whose solution is identified with the corresponding language/predicate
#### Example: Satisfiability Problem

Fix a set of propositional variables $\{ p_0, p_1, p_2, ... \} = Prop$

##### Formulas:
$$A, B, ...,  ::= p_i \ |\  \neg A \ | \ A \vee B \ | \ A \land B$$

##### Assignment:
$$\alpha : Prop \rightarrow \{ 0, 1 \}$$
##### Evaluation:
$$\alpha (\neg A) = 1 - \alpha (A)$$
$$\alpha (A \vee B) = max(\alpha(A), \alpha(B) )$$
$$\alpha(A \land B) = min(\alpha(A),  \alpha(B))$$

SAT is the set of formulas A such that $\exists \alpha . \alpha (A) = 1$ 

# Time Complexity
We often count time complexity as the number of basic operations on the data structure at hand. Examples of steps include:
- checking whether there is an edge between two nodes in a graph
- checking whether the $i$th bit of a binary string is 1 or 0
- checking (in)equality of two pieces of data
- checking that a string is a well-formed term of some grammar
- computing the sum, or even product of two natural numbers

#### Example: Satisfiability
Cost of evaluation:
- Each connection takes one time step
- Evaluating a formula under an assignment
- Takes time $O(n)$

#### Example: Sorting
##### Problem
Input: string of natural numbers $\sigma : (n_1, n_2, ..., n_k)$

Determine if $\sigma$ is sorted, i.e. $\forall i < k \ (n_i < n_{i+1})$

One possible algorithm: check for each i, $n_i < n_{i+1}$

This is a linear time algorithm: O(n)

### Polynomial Time
It is the class of problems for which there exists an algorithm that decides that problem in polynomial time

>[!info] Definition
>We say that an algorithm $A(x)$ decides a predicate $L \subseteq \{0, 1\}^*$ in time $O(f(n))$ if for each instance $x \in \{ 0, 1 \}^*$ , $A(x)$ terminates after $O(f|x|)$ basic steps of computation accepts if and only if $x \in L$

From this, <span style="color:#00bfff">polynomial-time computation</span> is defined as expected:

>[!info] Definition
>$P$ is the set of $L \subseteq \{ 0, 1 \}^*$ such that there is some polynomial $p(n)$ and an algorithm $A(x)$ deciding $L$ in $O(p(n))$ steps

##### Evaluation Problem
Another way of writing it:
$$\{ \ (A, \alpha ) : \alpha (A) = 1 \ \}$$
From earlier we know the algorithm is $O(n)$

$\therefore$ Eval $\in$ P

##### Sat problem

Sat $\in_?$ P

We don't know if it is solvable in polynomial time

#### Example: Reachability
Formally, a directed graph $G$ is given by:

$$G = (V, E \subseteq V \times V)$$
If you have 2 nodes $(s, t)$

Reach is defined as
$$Reach = \{ \ (G, s \in V, t \in V) : \text{there is a path from s to t in V}\}$$

**NB:** Any node can reach itself

Potential Algorithm: Calculate $E^1, E^2, E^3 ...$ progressively where $E^i$ is the graph of i-reachability
Then $s$ reaches $t$ iff $(s, t) \in E_{|r|}$
$\therefore$ reach $\in P$

### Closure of $P$ under Boolean combinations

Suppose $L_1, L_2 \in P$. Then also
1. $L^c_1 = \{ x \notin L_1 \} \in P$
2. $L_1 \cup L_2 \in P$
3. $L_1 \cap L_2 \in P$

<span style="color:#00bfff">Note, </span>$\textcolor{#00bfff}{L^c}$ <span style="color:#00bfff">means the complement of L</span>
#### Proof
Let $A_1(x), A_2(x)$ be algorithms deciding $L_1, L_2$ respectively in polynomial time: $O(n^k)$ where $k = max(k_1, k_2)$
1. Run $A_1(x$) and take the complement of the result - still $O(n^{k_1})$
2. Run $A_1(x)$ and:
	1. If accepts, accept
	2. If rejects, run $A_2(x)$
		1. If accepts, accept
		2. If rejects, reject
	- This is $O(n^{k_1}) + O(n^{k_2}) = O(n^k)$
3. Very similar to (2)

# Nondeterministic computation
In nondeterministic computational models, a program is allowed to make ‘guesses’ in the course of computation

We use an equivalent definition via the notion of 'certificate':
> [!info] Definition
> **NP** is the set of languages $L \subseteq \{ 0, 1 \}^*$ for which there is a polynomial-time algorithm $A(x, y)$ and a polynomial $p(n)$ such that
> $$x \in L \iff \exists y. (|y| < p(|x|) \ and \ A(x, y) \ accepts$$
> For a given $x \in L$, we may call such a witness $y$ the **certificate** of acceptance. The algorithm $A(x, y)$ is the **verifier**

For this we only need to 'guess' the certificate

#### Example: Satisfiability

SAT = $\{ Boolean \ formula \ | \ \exists x . assignment\  \alpha(A) = 1 \}$

#### Example: Clique
A clique is a set of nodes C such that $\forall u, v \in C \ distinct: (u - v \ in \ G)$

K-Clique = $\{ (G, K) : \text{G has a clique of size K and } K \in \mathbb{N}$

Another way of saying this is 
$(G, K) \in K-Clique \iff \exists C \text{ set of nodes in G of size} \geq K \ (\forall u, v \in C \ distinct \ u-v \ in \ G)$
In this $C$ is out certificate
$\text{ set of nodes in G of size} \geq K$ is of polynomial size
$\forall u, v \in C \ distinct u-v \ in \ G$ is out verifier
### Closure of $NP$ under positive Boolean combinations

Suppose $L_1, L_2 \in NP$. Then also
1. $L_1 \cup L_2 \in NP$
2. $L_1 \cap L_2 \in NP$

#### Proof
Let $A_1 (x, y), A_2 (x, y)$ be the verifiers and $P_1 (n) and p_2 (n)$ to be the provers for $L_1, L_2$ respectively

1. $x \in L_1 \cup L_2 \iff x \in L_1 \ or \ x \in L_2$
	1. $\iff \exists y_1 . (|y_1| < p_1(|x|) \ and \ A_1 (x, y_1) \ accepts)$ OR
			$\exists y_2 . (|y_2| < p_2(|x|) \ and \ A_2 (x, y_2) \ accepts)$
	2. $\iff \exists y (|y| < p_1(|x|) + p_2 (|x|)$ and $A_1 (x, y) \ accepts$ or $A_2(x, y) \ accepts$
	

# Polynomial-time reductions
A reduction, as in mathematics, is a way of saying that one problem is ‘as hard’ as another. For complexity theory, we require the reduction itself to be efficiently computed:

>[!info] Definition
>Fix languages $L, L' \subseteq \{0, 1 \}^*$. A **polynomial-time reduction** from $L$ to $L'$ is a function $f: \{ 0, 1\}^* \rightarrow \{ 0, 1 \}^*$ such that:
>- $F$ if polynomial-time, i.e. we can compute $F(x)$ in a number of steps polynomial to $|x|$
>- $x \in L \iff f(x) \in L'$
>
>We write $L \leq_p L'$ when there is a polynomial-time reduction from $L$ to $L'$


#### Example: reducing Independent-Set to Clique
K-IndSet = $\{ (G, K) : \exists I \leq \text{G of size} \geq K (\forall u, v \in I \ distinct \  \text { no edge from u to v in G }$

Reduction from K-IndSet to K-Clique:
Define $f : (G, K) \longrightarrow (\bar{G}, K)$
- $\bar{G}$ is $G$ with all edges flipped

We know $f$ is polytime
$(G, K) \in K-IndSet \Rightarrow \exists \text{a K-IndSet C in G}$
				  $\Rightarrow \exists \text{a K-Clique C in } \bar{G}$
				  $\Rightarrow (\bar{G}, K) \in K-Clique$

Proving the other way round is very similar


### $NP$-hardness

>[!info] Definition
>$L \subseteq \{ 0, 1 \}^* is **NP-hard** if for every $L' \in NP$ we have $L' \leq_p L$.
>Furthermore, if $L \in NP$, then we say that $L$ is **NP-complete**

NP-complete problems are the 'hardest' problems in NP. They are 'as hard' as any other NP problem

**NB:** all languages in NP are decidable, in particular in exponential time



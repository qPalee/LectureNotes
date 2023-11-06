[[Relations]] from a set to itself, from A to A, is an **endorelation** on A
[[Functions]] from a set to itself, from A to A, is an **endofunction** on A -> $x^2$ is an endofunction on $x$

A directed graph is a finite set with an endorelation
The elements are called verices/nodes and the ordered pairs in the relationa re called edges/arrows

Note: this definition implies that a directed graph can have roots but cannot have more than one edge from x to y
An edge doesnt have a multiplicity

## RST (Reflexity, Symmetric Transitive) Properties
- A relation R is **reflexive** when everything is related to itself (Every vertex has a loop)
- A relation R is **symmetric** when $\forall \space x, y \in A$, if x is related to y, then y is related to x
- A relation R is **transitive** when $\forall \space x, y, z \in A$, if x is related to y and y is related the z, then x is related to z

A relation that is reflexive, symmertic and transitive is called an **equivalent relation**

$x \cong y (mod 10)$ is an equivalent realtion on integers

If is an equivalent relation on A, each element $x \in a$  has a equivalence class

$[x]_\equiv = {}$

Note that:
- Every $x \in A$ belongs to its own equivalence class
- If $x = y$, then they have the same equivalence class
- If $x \neq y$, then $[x]_\equiv$ and $[y]_\equiv$ are disjoint sets (nothing in common)
- The set of all equivalence classes is a/$\equiv$
- A quotient set doesn't contain the empty set, $\emptyset$

Take set integers and $\cong$ (mod 10), 
$[7]_{\equiv (mod 10)}$ = {7, 17, 27, ...}

A partition of a set A is a set B of subsets
- any two distinct members are disjoint
- every element of A belongs to some subset of B
- A/$\equiv$ is **always** a partition
- Every partition of a set gives us an equivalence relation

We have a one-to-one correspondence between the equivalence relations on A and the partitions of A

Given a function F from A to B,
The range of F is the set of elements of B with at least 1 preimage
The kernel of F is the equivalence relation on A that {(x, y) $\in$ AxA | f(x) = f(y)}

$\frac{A}{kernel(F)}$ is in a one-to-one correspondence to the range of F

A relation A is irreflexive when nothing is related to itself (no loops)

A realtion on A is antisymmetric when $\forall \space x, y \in A$, $(x \neq y) \implies \lnot(x R y + y R x)$, 

$\subseteq$ is an order of $\wp$ X

x | y is an order on the set of natural numbers, not an order on the set of integers bc 3|-3 and -3|3 but $3 \neq -3$ 

An order is depicted by a Hasse Diagram
No need to draw inferrable edges

In an ordered set, two elements are comparable when either x=y $\lor$ xRy $\lor$ yRx

If any two elements are comparable, then R is a linear order
$\leq$ on natural numbers is a linear order
$\subseteq$ on $\wp X$ 
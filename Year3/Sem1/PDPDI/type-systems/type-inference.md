# Type Inference

### Type Checking vs Type Inference
The typing rules of the Simply Typed $\lambda$-calculus allow checking that expressions are well-typed.

Type inference is the process of inferring the types of an expression without type annotations so that it type checks according to given typing rules

Can we use the Curry-style Simply Typed $\lambda$-calculus for type inference?
- No, the `ABS` rule doesn't tell us how to pick $x$'s type $T$
- To infer that type we need to know how $x$ is used
	- We need to inspect $M$

#### Constraint-based Type Inference
Instead of trying to guess the type of $\lambda$-abstractions' arguments, algorithms generate <span style="color:#00bfff">type variables</span> that are later refined when more information is available

These algorithms split the process of reconstructing types into 2 parts:
1. Generate type constraints involving type variables in a syntax-directed way
2. Solve the set of generated constraints

This delays the decision of picking a type until the entire expression has been analysed so that the necessary information to make this decision is available

##### Type, type variables, and type constraints
- We extend the syntax of types with type variables of the form $\textcolor{#00bfff}{\alpha : T ::= \alpha \space | |space \mathbb{B} \space | \space T \rightarrow T}$
- Type constraints are equalities of the form $\textcolor{#00bfff}{T_1 = T_2}$
- We use $\textcolor{#00bfff}{C}$ to denote sets of type constraints

#### Wand's algorithm
##### Interface + state
- <span style="color:#00bfff">Input</span>: a term
- <span style="color:#00bfff">State</span>:
	- a set of type constraints $\textcolor{#00bfff}{C}$
	- a set of goals $\textcolor{#00bfff}{G}$ of the form $\textcolor{#00bfff}{<\Gamma;M;T>}$
- <span style="color:#00bfff">Output</span>: $\textcolor{#00bfff}{C}$
##### Algorithm
- <span style="color:#00bfff">Input</span>: a term $\textcolor{#00bfff}{M_0}$ without type annotations
- <span style="color:#00bfff">Initialization</span>:
	- Set $\textcolor{#00bfff}{C = \emptyset}$
	- Set $\textcolor{#00bfff}{G = \{<\Gamma_0;M_0;\alpha_0>\}}$ where
		- $\textcolor{#00bfff}{\alpha_0}$ is a fresh type variable
		- $\textcolor{#00bfff}{\Gamma}$ maps $\textcolor{#00bfff}{M_0}$'s free variables to distinct fresh type variables
##### Loop Step
- if $\textcolor{#00bfff}{G=\emptyset}$ return $\textcolor{#00bfff}{C}$
- else
	- choose a goal $\textcolor{#00bfff}{<\Gamma;M;T>}$ in $\textcolor{#00bfff}{G}$ and remove it
	- apply the <span style="color:#00bfff">action table</span> to $\textcolor{#00bfff}{<\Gamma;M;T>}$
	- add the returned type constraints and goals to $\textcolor{#00bfff}{C}$ and $\textcolor{#00bfff}{G}$

#### Using the result of Wand's algorithm
- Given a term $\textcolor{#00bfff}{M-0}$, this algorithm
	- Returns a set of type constraints $\textcolor{#00bfff}{C}$
	- Where $\textcolor{#00bfff}{\alpha_0}$ stands for $\textcolor{#00bfff}{M-0}$'s type
##### Solve $\textcolor{#00bfff}{C}$
If it is solvable
- the solver produces a substitution $\textcolor{#00bfff}{S}$
- such that $\textcolor{#00bfff}{\Gamma_0[S] \vdash M_0 " \alpha_0[S]}$
If it is not solvable, $\textcolor{#00bfff}{M_0}$ is not well-typed

##### Applying substitutions
$\textcolor{#00bfff}{X[S]}$ replaces all occurrences of $\textcolor{#00bfff}{\alpha_i}$ with $\textcolor{#00bfff}{T_i}$ in $\textcolor{#00bfff}{X}$
###### Example
$$\textcolor{#00bfff}{(\alpha_1 \rightarrow \alpha_2)[\alpha_1 \mapsto \mathbb{B}, \alpha_2 \mapsto \mathbb{B} \rightarrow \mathbb{B}] = \mathbb{B} \rightarrow (\mathbb{B} \rightarrow \mathbb{B})}$$
If $\textcolor{#00bfff}{\alpha}$ occurs several times in a substitution, the last one is used 

#### Action Table
The action table
- takes a goal of the form $\textcolor{#00bfff}{<\Gamma;M;T>}$
- and returns a pair of a set of constraints $\textcolor{#00bfff}{C}$ and a set of sub-goals $\textcolor{#00bfff}{G}$

##### Action Rules
![[Pasted image 20241024195611.png]]


We say x has type $\alpha$ until we can infer what type it actually is
There can be multiple different $\alpha$s


# Simply-Typed $\lambda$-calculus
### Types
Types are used to help explain the meaning of terms

For example, if we can assign the type $N$ to an expression then we know that it computes to a number without evaluating it

Types:
- provide guarantees on how terms compute
- typed expressions <span style="color:#00bfff">do not get stuck</span>
- document the code
- provide optimisations

Type checking is the process of checking that some given expression has some given type w.r.t given typing rules

In general, type checking provides a lightweight verification technique

### Syntax of the Simply Typed $\lambda$-calculus

It is a typed variant of the untyped $\lambda$-calculus
- It is built on top of a collection of ground types
- We only consider a single ground type: <span style="color:#00bfff">Booleans</span> $\textcolor{#00bfff}{(\mathbb{B})}$
- The only other type is the type of functions (such as $\textcolor{#00bfff}{\mathbb{B} \rightarrow \mathbb{B}}$)

#### Syntax of simple types
$$\textcolor{#00bfff}{T ::= \mathbb{B} \text{ | } T \rightarrow T}$$
#### Syntax of terms
$$\textcolor{#00bfff}{M ::= x \space | \space \lambda .x : T.M \space | \space M \space M \space | \space true \space | \space false \space | \text{ if M then M else M}}$$

##### Notes
- We add two Boolean constants and one operation to make the examples more interesting - these are primitives
- A $\lambda$-abstraction $\textcolor{#00bfff}{\lambda x \space : \space T.M}$ mentions the type $\textcolor{#00bfff}{T}$ of its argument
- Convention: $\rightarrow$ is associative to the right (i.e., $\textcolor{#00bfff}{T_1 \rightarrow T_2 \rightarrow T_3 \text{ stands for } T_1 \rightarrow (T_2 \rightarrow T_3)}$
##### Examples

###### Types
- $\textcolor{#00bfff}{\mathbb{B}}$
- $\textcolor{#00bfff}{\mathbb{B} \rightarrow \mathbb{B}}$
- $\textcolor{#00bfff}{(\mathbb{B} \rightarrow \mathbb{B}) \rightarrow \mathbb{B}}$
- $\textcolor{#00bfff}{(\mathbb{B} \rightarrow \mathbb{B}) \rightarrow (\mathbb{B} \rightarrow \mathbb{B})}$
###### Terms
- $\textcolor{#00bfff}{\lambda x \space : \space \mathbb{B} . \text{if x then false else true}}$
- $\textcolor{#ff0000}{\lambda x \space : \space \mathbb{B} . \lambda y \space : \space \mathbb{B} \rightarrow \mathbb{B}. \text{ if x then x else y}}$
	- This is not allowed since the type of $x$ and the type of $y$ are not the same

In lambda abstractions, we are gonna declare the type of the bound variable

In an `if then else` we will only allow it if both the possible outputs are of the same type

### Small-step call-by-value operational semantics
#### Values
$$\textcolor{#00bfff}{V ::= \lambda x \space : \space T.M \space | \text{ true } |\text{ false}}$$
#### Evaluation contexts
$$\textcolor{#00bfff}{C ::= \huge \cdot \normalsize \space | \space C \space M \space | \space V \space C \space | \text{ if C then M else M}}$$
#### Rules
$$\textcolor{#00bfff}{\cfrac{}{(\lambda x \space : \space T.M) V \longrightarrow_v M[x\text{\\}V]}\beta}$$
$$\textcolor{#00bfff}{\cfrac{}{\text{if true then M else N} \longrightarrow_v M}IteT}$$
$$\textcolor{#00bfff}{\cfrac{}{\text{if true then M else N} \longrightarrow_v N}IteT}$$
$$\textcolor{#00bfff}{\cfrac{M \longrightarrow_V N}{C[M] \longrightarrow_v C[N]}CTX_C}$$
### Typing 
The simply types $\lambda$-Calculus includes typing rules that associate types with expressions

<span style="color:#00bfff">Type judgements</span> are derived with the form $\textcolor{#00bfff}{\Gamma \vdash M:T }$ where a typing environment $\Gamma$ is a partial map from variables to types.
- Types are given to the free variables of $\textcolor{#00bfff}{M}$
- They are written in the form $\textcolor{#00bfff}{x_1 : t_1, ..., x_n:T_n}$
- It maps each $\textcolor{#00bfff}{x_i}$ to $\textcolor{#00bfff}{T_i}$ ($\textcolor{#00bfff}{\Gamma (x_i) = T_i}$)
- $\textcolor{#00bfff}{dom(\Gamma) = \{x_1, ..., x_n\}}$
- Let $\textcolor{#00bfff}{}$$\textcolor{#00bfff}{\Gamma, x:T}$ be the context that
	- maps $\textcolor{#00bfff}{x}$ to $\textcolor{#00bfff}{T}$
	- allows each $\textcolor{#00bfff}{y \in dom(\Gamma)}$ such that $\textcolor{#00bfff}{y \neq x}$ to $\textcolor{#00bfff}{\Gamma(y)}$

##### Examples
- An environment: $\textcolor{#00bfff}{x:\mathbb{B}, y : \mathbb{B}}$
- $\textcolor{#00bfff}{x:\mathbb{B}, y : \mathbb{B}, x:\mathbb{B} \rightarrow \mathbb{B}}$ is $\textcolor{#00bfff}{y:\mathbb{B}, x:\mathbb{B} \rightarrow \mathbb{B}}$
	- Variable names are never repeated
	- If they are then the last instance of that variable is used

A lambda abstraction term cant be a boolean value, must be a function
#### Rules
$$\textcolor{#00bfff}{\cfrac{}{\Gamma, x:T \vdash x:T}VAR}$$
$$\textcolor{#00bfff}{\cfrac{\Gamma, x:T \vdash M:U}{\Gamma \vdash \lambda x:T.M : T\rightarrow U}ABS}$$
$$\textcolor{#00bfff}{\cfrac{\Gamma \vdash M:T \rightarrow U \quad \Gamma \vdash N:T}{\Gamma \vdash M \space N:U}APP}$$
$$\textcolor{#00bfff}{\cfrac{}{\Gamma \vdash true : \mathbb{B}}T}$$
$$\textcolor{#00bfff}{\cfrac{}{\Gamma \vdash false : \mathbb{B}}F}$$
$$\textcolor{#00bfff}{\cfrac{\Gamma \vdash M:\mathbb{B} \quad \Gamma \vdash N:T \quad \Gamma \vdash P:T}{\Gamma \vdash \text{if } M \text{ then } N \text{ else } P:T}ITE}$$

#### Proof
![[Pasted image 20241021123242.png]]
We can use the empty set since there are no free variables

![[Pasted image 20241021123257.png]]
what the fuck is this
i kinda understand this but omg its ugly
### Expressive Power
"Typed expressions do not get stuck"

Examples of expressions that do not have types and get stuck
- $\textcolor{#00bfff}{true \space true}$
- $\textcolor{#00bfff}{\text{if} (\lambda x : \mathbb{B}.x) \text{ then } true \text{ else } false}$

What type can $\textcolor{#00bfff}{\lambda x: T.xx}$ be assigned?
$$\textcolor{#00bfff}{\cfrac{x:T \vdash x:T \rightarrow U \quad x:T \vdash x:T}{\cfrac{x:T \vdash xx:U}{\vdash \lambda x:T.xx : T \rightarrow U}\tiny{ABS}}\tiny{APP}}$$
We cannot complete this proof as $\textcolor{#00bfff}{x}$ would have to have both type $\textcolor{#00bfff}{T \rightarrow U}$ and type $\textcolor{#00bfff}{T}$

This type system guarantees that types expressions do not get stuck
It also prevents us from typing some expressions that do not get stuck
- It is no longer Turning-complete

#### Properties
##### Uniqueness
in a given context $\textcolor{#00bfff}{\Gamma}$, a term $\textcolor{#00bfff}{M}$ (with free variables all in $\textcolor{#00bfff}{dom(\Gamma)}$) has at most one type, and one derivation that it has this type
##### Canonical Form
A value of type $\textcolor{#00bfff}{\mathbb{B}}$ is either $\textcolor{#00bfff}{true}$ or $\textcolor{#00bfff}{false}$, and a value of type $\textcolor{#00bfff}{T \rightarrow U}$ is of the form $\textcolor{#00bfff}{\lambda x:T.M}$
##### Progress
A closed well-typed term $\textcolor{#00bfff}{M}$ either is a value or it can be reduced further
- There exists $\textcolor{#00bfff}{N}$ such that $\textcolor{#00bfff}{M \longrightarrow_v N}$
##### Substitution
If $\textcolor{#00bfff}{\Gamma, x:U \vdash M:T}$ and $\textcolor{#00bfff}{\Gamma \vdash N:U}$ then $\textcolor{#00bfff}{\Gamma \vdash M[x\text{\\} N]:T}$
##### Preservation
If $\textcolor{#00bfff}{\Gamma \vdash M:T}$ and $\textcolor{#00bfff}{M \longrightarrow_v T}$ then $\textcolor{#00bfff}{\Gamma \vdash N:T}$
##### Safety = Progress + Preservation
Well types terms do not get stuck

<span style="color:#ff0000">Not expected to learn the proofs of these properties</span>

### Church-style vs Curry-style

#### Grammar of the Curry-Style Simply Typed $\lambda$-calculus
$$\textcolor{#00bfff}{T ::= \mathbb{B}  \space | \space T \rightarrow T}$$
$$\textcolor{#00bfff}{M ::= x \space |} \textcolor{#ff0000}{\space \lambda x.M \space } \textcolor{#00bfff}{| \space M \space M \space | \space true \space | \space false \space | \text{ if M then M else M}}$$

Curry-Style has important consequences:
- <span style="color:#00bfff">Uniqueness</span> is no longer true
	- $\textcolor{#00bfff}{\lambda x.x}$ can be assigned any type of the form $\textcolor{#00bfff}{T \rightarrow T}$
#### Curry-Style Simply Typed $\lambda$-Calculus' $\lambda$-abstraction rule
The only rule that differs is the $\lambda$ abstraction rule
We use $\textcolor{#00bfff}{\Gamma \vdash_i M:T}$ for this calculus
$$\textcolor{#00bfff}{\cfrac{\Gamma, x:T \vdash_i M:U}{\Gamma \vdash_i \lambda x.M : T \rightarrow U}\tiny{ABS}}$$
#### Erasure function
The two calculi are related through the <span style="color:#00bfff">erasure</span> function

$\textcolor{#00bfff}{erase(x) = x}$
$\textcolor{#00bfff}{erase(\lambda x:T.M) = \lambda x.erase(M)}$
$\textcolor{#00bfff}{erase(M \space N) = erase(M) \space erase(N)}$
$\textcolor{#00bfff}{erase(true) = true}$
$\textcolor{#00bfff}{erase(false) = false}$
$\textcolor{#00bfff}{erase(\text{if } M \text{ then } N \text{ else } P) = \text{if } erase(M) \text{ then } erase(N) \text { else } erase(N)}$

Erasure property:
- if $\textcolor{#00bfff}{\Gamma \vdash M:T}$ then $\textcolor{#00bfff}{\Gamma \vdash_i erase(M):T}$

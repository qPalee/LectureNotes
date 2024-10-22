q# Small Step Operational Semantics
Small step operational semantic are similar to big step but instead it specifies how programs execute 1 step at a time

Small-step semantics overcomes the shortcomings of big-step

### Call-by-value
<span style="color:#00bfff">Values</span> ($\lambda$-abstractions of the form $\textcolor{#00bfff}{\lambda x.M}$) are denoted by <span style="color:#00bfff">V</span>
#### $\beta$-rule
$$\cfrac{}{(\lambda x.M ) \space V \longrightarrow_v m[x \text{\\} V]}\beta$$
#### Context rules
$$\cfrac{M \longrightarrow_v P}{M \space N \longrightarrow_v P \space N}APP_1$$
$$\cfrac{M \longrightarrow_v P}{V \space M \longrightarrow_v V \space P}APP_2$$
Let $\longrightarrow_{v}^{*}$ be the reflexive and transitive closure of $\longrightarrow_v$

![[Pasted image 20241017175405.png]]
![[Pasted image 20241017175426.png]]

### Call-by-name
Arguments of functions are only evaluated when used
#### $\beta$-rule
$$\cfrac{}{(\lambda x.M) \space N \longrightarrow_n M[x \text{\\}N]}\beta$$
#### Context rule
$$\cfrac{M \longrightarrow_n P}{M \space N \longrightarrow_n P \space N}APP$$
### Properties
##### Values
- If $\textcolor{#00bfff}{M \Longrightarrow_v N}$ then $\textcolor{#00bfff}{N}$ is a $\lambda$-abstraction
- If $\textcolor{#00bfff}{M \Longrightarrow_n N}$ then $\textcolor{#00bfff}{N}$ is a $\lambda$-abstraction
##### Deterministic
- If $\textcolor{#00bfff}{M \Longrightarrow_v N}$ and $\textcolor{#00bfff}{M \Longrightarrow_v P}$ then $\textcolor{#00bfff}{N=P}$
- If $\textcolor{#00bfff}{M \Longrightarrow_n N}$ and $\textcolor{#00bfff}{M \Longrightarrow_n P}$ then $\textcolor{#00bfff}{N=P}$
##### $\beta$-equality
- If $\textcolor{#00bfff}{M \Longrightarrow_v N}$ then $\textcolor{#00bfff}{M =_{\beta} N}$
- If $\textcolor{#00bfff}{M \Longrightarrow_n N}$ then $\textcolor{#00bfff}{M =_{\beta} N}$

Using [[evaluation-contexts]], the small-step semantics of the untyped pure $\lambda$-calculus can be rephrased as follows
![[Pasted image 20241022113944.png]]

### Normal Forms
A normal form (wrt a transition system) is one that cannot be reduced further
A term that has a normal form is said to <span style="color:#00bfff">converge</span> otherwise it is said to <span style="color:#00bfff">diverge</span>

A normal form that is not a value is said to be <span style="color:#00bfff">stuck</span>

Different strategies might lead to different convergence behaviours and different normal forms
- $\textcolor{#00bfff}{(\lambda y. \lambda x.x)(\Delta \Delta)}$
	- call-by-value: <span style="color:#ff0000">diverges</span>
	- call-by-name: $\textcolor{#00ff00}{\text{converges to } \lambda x.x}$
- $\textcolor{#00bfff}{(\lambda x.\lambda y.x)((\lambda z.z)(\lambda w.w))}$
	- call-by-value: $\textcolor{#00ff00}{\text{converges to } \lambda y. \lambda w.w}$
	- call-by-name: $\textcolor{#00ff00}{\text{converges to } \lambda y.(\lambda z.z)(\lambda w.w)}$
- $\textcolor{#00bfff}{\lambda y. (\lambda z.z)(\lambda w.w)}$
	- call-by-value: $\textcolor{#00ff00}{\text{is already a value}}$
	- call-by-name: $\textcolor{#00ff00}{\text{is already a value}}$

If a term converges using call-by-value, then it converges using call-by-name
- this is not true for the other way around though

Not all strategies reduce all $\beta$-redexes in normal forms
- A $\beta$-normal form is a $\lambda$-term without $\beta$-redexes

#### Normal order reduction
Normal order reduction is a strategy where normal forms are all $\beta$-normal forms

It reduces leftmost outermost $\beta$-redexes first

If $\textcolor{#00bfff}{M}$ is $\beta$-equal to a $\beta$-normal form $\textcolor{#00bfff}{N}$, then the normal order reduction reduces $\textcolor{#00bfff}{M}$ to $\textcolor{#00bfff}{N}$

Call-by-name converges whenever normal order converges

Normal order reduction is defined as follows
$$\textcolor{#00bfff}{\cfrac{}{x \Longrightarrow_{no} x}}$$
$$\textcolor{#00bfff}{\cfrac{M \Longrightarrow_{no} N}{\lambda x.M \Longrightarrow_{no} \lambda x.N}}$$
$$\textcolor{#00bfff}{\cfrac{M \Longrightarrow_n \lambda x.P \quad P[x \text{\\}N] \Longrightarrow_{no} Q}{M \space N \Longrightarrow_{no} Q}}$$
$$\textcolor{#00bfff}{\cfrac{M \Longrightarrow_n P \neq \lambda x.T \quad M \Longrightarrow_{no} Q \quad N \Longrightarrow_{no} R}{M \space N \Longrightarrow_{no} Q \space R}}$$

##### Example
- $\textcolor{#00bfff}{(\lambda x. \lambda y. y)(\lambda x.xx)(\lambda x.xx) \Longrightarrow_{no} \lambda y.y}$
	- This does not reduce to a normal form

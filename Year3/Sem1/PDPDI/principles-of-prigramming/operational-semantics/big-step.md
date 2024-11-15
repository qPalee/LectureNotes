# Big-Step Operational Semantics

Operational Semantics specify the behaviour of programs be describing how they execute on abstract machines that perform steps of computations

You can tell what rules to apple by looking at the syntax

It specifies how programs execute in one step

### Transition System
All it needs is a set of states and a binary transition relation between states

Our states will simply be $\lambda$-terms

The transition relation can be defined as a proof system consisting of derivation rules

We will only do big step operational semantics on closed programs

Values will always be terms of lambda abstractions
Lambda term is a terminal state in a machine

A big-step semantics specifies how terms compute to values in 1 step
Values are $\lambda$-abstractions of the form $\lambda x.M$

##### 1st rule
$$\cfrac{}{\lambda x.M \Longrightarrow_v \lambda x.M}VAL$$
##### 2nd rule
$$\cfrac{M \Longrightarrow_v \lambda x.P \quad N \Longrightarrow_v Q \quad P[x \text{\\} Q] \Longrightarrow_v V}{M \space N \Longrightarrow_v V}APP$$

Notes: 
- $M \Rightarrow_v N$ only when $N$ is a $\lambda$-abstraction
- Reductions are not allowed inside $\lambda$s

The small steps are all hidden

#### Example
![[Pasted image 20241015103207.png]]
![[Pasted image 20241015103215.png]]

### Evaulaltion Strategies
We are doing a call-by-value strategy, where arguments to functions are always evaluated whether or not they are used 
- before $\beta$-reducing $(\lambda x.M) N$, the argument $N$ must first be computed to a value

An evaluation strategy fixes the order in which reduced must be reduced

#### Call-by-name
Call-by-name is another strategy where args aren't evaluated until they are actually needed

##### 1st rule
$$\cfrac{}{\lambda x.M \Longrightarrow_n \lambda x.M}VAL$$
##### 2nd rule
$$\cfrac{M \Longrightarrow_n \lambda x.P \quad P[x \text{\\} N] \Longrightarrow_n V}{M \space N \Longrightarrow_n V}APP$$
Note: Once again, $M \Longrightarrow_n N$ only when $N$ is a $\lambda$-abstraction

#### Properties
##### Values
- If $\textcolor{#00bfff}{M \Longrightarrow_v N}$ then $\textcolor{#00bfff}{N}$ is a $\lambda$-abstraction
- If $\textcolor{#00bfff}{M \Longrightarrow_n N}$ then $\textcolor{#00bfff}{N}$ is a $\lambda$-abstraction
##### Deterministic
- If $\textcolor{#00bfff}{M \Longrightarrow_v N}$ and $\textcolor{#00bfff}{M \Longrightarrow_v P}$ then $\textcolor{#00bfff}{N=P}$
- If $\textcolor{#00bfff}{M \Longrightarrow_n N}$ and $\textcolor{#00bfff}{M \Longrightarrow_n P}$ then $\textcolor{#00bfff}{N=P}$
##### $\beta$-equality
- If $\textcolor{#00bfff}{M \Longrightarrow_v N}$ then $\textcolor{#00bfff}{M =_{\beta} N}$
- If $\textcolor{#00bfff}{M \Longrightarrow_n N}$ then $\textcolor{#00bfff}{M =_{\beta} N}$

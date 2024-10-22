# Evaluation Contexts
Although the untyped pure $\lambda$-calculus' small-step semantics only has
- 2 context rules in call-by-value
- 1 context rule in call-by-name
Real world programming languages can have many more

Evaluation contexts provide a way to compactly express context rules
An evaluation context is a term which a special variable $\Huge{\cdot}$, called the <span style="color:#00bfff">hole</span>

If $\textcolor{#00bfff}{C}$ is an evaluation context, then $\textcolor{#00bfff}{C[M]}$ represents $\textcolor{#00bfff}{C}$ with $\textcolor{#00bfff}{M}$ substituted for $\textcolor{#00bfff}{\Huge{\cdot}}$

Every evaluation context $\textcolor{#00bfff}{C}$ represents a context rule
$$\textcolor{#00bfff}{\cfrac{M \longrightarrow_v N}{C[M] \longrightarrow_v C[N]}}$$
expressing that $\textcolor{#00bfff}{M}$ can be reduced to $\textcolor{#00bfff}{N}$ in the context $\textcolor{#00bfff}{C}$

#### Values
Values are $\lambda$-abstractions of the form $\textcolor{#00bfff}{\lambda x.M}$ and are denoted by $\textcolor{#00bfff}{V}$
#### Call-by-name evaluation contexts
$$\textcolor{#00bfff}{C ::=  \Huge \cdot \normalsize \space | \space C \space M \space | \space V \space C}$$
#### Call-by-value evaluation contexts
$$\textcolor{#00bfff}{C::= \huge \cdot \normalsize \space | \space C \space M}$$

**Note:** we use the same context notation as it will be clear from the context whether we mean call-by-value or call-by-name contexts


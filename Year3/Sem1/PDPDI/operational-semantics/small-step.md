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


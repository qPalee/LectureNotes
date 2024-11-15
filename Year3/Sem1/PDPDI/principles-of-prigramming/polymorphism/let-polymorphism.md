# Let-Polymorphism
We are going to extend out curry-style language to include numbers and let-expressions

#### Syntax
$$\textcolor{#00bfff}{T ::= \alpha \text{ } | \text{ } \mathbb{B} \text{ } | \text{ }} \textcolor{#ff0000}{\mathbb{N}} \textcolor{#00bfff}{ \text{ } | \text{ } T \rightarrow T}$$
$$\textcolor{#00bfff}{M ::= x \text{ } | \text{ } \lambda x.M \text{ | } M \text{ } M \text{ | } true \text{ | } false \text{ | if } M \text{ then } M \text{ else } M \text{ | }}$$
$$\textcolor{#ff0000}{\text{let } x = M \text{ in } M \text{ | } zero \text{ | } succ \text{ } M \text{ | } pred \text{ } M \text{ | } iszero \text{ } M}$$
#### Values
$$\textcolor{#00bfff}{V ::= \lambda x.M \text{ | } true \text{ | } false \text{ | }} \textcolor{#ff0000}{zero \text{ | } succ \text{ } V}$$
#### Call-by-value evaluation contexts
$$\textcolor{#00bfff}{C ::= \Huge \cdot \normalsize \ | \ C \ M \ | \ V \ C \ | \ \text{if } C \text{ then } M \text{ else } M}$$
$$\textcolor{#ff0000}{| \ \text{let }x=C \text{ in } M \ | \ pred \ C \ | \ iszero \ C \ | \ succ \ C}$$
#### Call-by-value small-step operational semantics rules
![[Pasted image 20241028163935.png]]

#### New typing rules
Wake up babe new typing rules just dropped
$$\textcolor{#00bfff}{\cfrac{}{\Gamma \vdash zero \ : \ \mathbb{N}}\Tiny Z}$$
$$\textcolor{#00bfff}{\cfrac{\Gamma \vdash M : \mathbb{N}}{\Gamma \vdash succ \ M : \mathbb{N}}\Tiny S}$$
$$\textcolor{#00bfff}{\cfrac{\Gamma \vdash M : \mathbb{N}}{\Gamma \vdash pred \ M : \mathbb{N}}\Tiny P}$$
$$\textcolor{#00bfff}{\cfrac{\Gamma \vdash M : \mathbb{N}}{\Gamma \vdash iszero \ M: \mathbb{B}}\Tiny I}$$
$$\textcolor{#00bfff}{\cfrac{\Gamma \vdash M : T \quad \Gamma ,x:T \vdash N : U}{\Gamma \vdash let \ x = M \ in \ N:U}\Tiny LET}$$

##### Why is $\textcolor{#00bfff}{(\lambda f.if \ (f \ true) \ then \ (f \ zero) \ else \ (f \ one)) (\lambda x.x)}$ not well typed?
- We cannot assign $\textcolor{#00bfff}{\mathbb{B} \rightarrow \mathbb{B}}$ to $\textcolor{#00bfff}{\lambda x.x}$ since $\textcolor{#00bfff}{f}$ is also applied to $\textcolor{#00bfff}{zero}$
- We cannot assign $\textcolor{#00bfff}{\mathbb{N} \rightarrow \mathbb{N}}$ to $\textcolor{#00bfff}{\lambda x.x}$ since $\textcolor{#00bfff}{f}$ is also applied to $\textcolor{#00bfff}{true}$
- We cannot assign $\textcolor{#00bfff}{\alpha \rightarrow \alpha}$ since $\textcolor{#00bfff}{\mathbb{B} \neq \mathbb{N}}$

We can make it well typed by using the let notation:


# Let-Polymorphism
We are going to extend out curry-style language to include numbers and let-expressions

#### Syntax
$$\textcolor{#00bfff}{T ::= \alpha \text{ } | \text{ } \mathbb{B} \text{ } | \text{ }} \textcolor{#ff0000}{\mathbb{N}} \textcolor{#00bfff}{ \text{ } | \text{ } T \rightarrow T}$$
$$\textcolor{#00bfff}{M ::= x \text{ } | \text{ } \lambda x.M \text{ | } M \text{ } M \text{ | } true \text{ | } false \text{ | if } M \text{ then } M \text{ else } M \text{ | }}$$
$$\textcolor{#ff0000}{\text{let } x = M \text{ in } M \text{ | } zero \text{ | } succ \text{ } M \text{ | } pred \text{ } M \text{ | } iszero \text{ } M}$$
#### Values
$$\textcolor{#00bfff}{V ::= \lambda x.M \text{ | } true \text{ | } false \text{ | }} \textcolor{#ff0000}{zero \text{ | } succ \text{ } V}$$
#### Call-by-value evaluation contexts
$$\textcolor{#00bfff}{C ::= \Huge \cdot \$$



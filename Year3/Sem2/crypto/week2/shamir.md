# Shamir Secret Sharing

### Polynomials

We can evaluate $f(x) = x^2 - 1$ over $\mathbb{Z}_3$ in which case $f(2) \equiv 0$

The degree of polynomial needs to be the number of users required

When working with modulo p, we always assume that exponents are strictly smaller than p

The set of polynomials over $\mathbb{Z}_p$ is a commutative ring:
- if we take 2 polynomials over $\mathbb{Z}_p$ then their sum exists
- their difference exists
- we can multiply 2 polynomials
- we can divide and have a remainder

Dividing $6x^4 + 8x + 1 by 2x^2 + 4 \text{ over } \mathbb{Z}_11 \text{ we get } (3x^2+5)(2x^2+4)+(8x+3)$


#### Properties
- A non-zero polynomial degree $d$ has at most $d$ roots
- Given d+1 pairs, there is a unique polynomial with degree d
- A polynomial with degree $d$ has $d+1$ coefficients, and $p$ choices for each coefficient
	- This means there is $p^{d+1}$ polynomials
	- We can have a small degree but have lots of polynomials

Even with only 1 coefficient secret, there is still $2^{128}$ possible polynomials
#### Reconstruction
![[Pasted image 20250127154512.png]]
 You can solve the polynomial with simultaneous equations

### Lagrange
Fancy looking maths going on here

Given $D+1$ pairs $(x_i, f(x_i))$, the Lagrange polynomials are constructed using $$\delta_i(x) = \frac{\Pi_{j \neq i }(x - x_j)}{\Pi_{j \neq i}(x_i - x_j)}$$
This only computes x coordinates, not y
If x == 1, then $\delta_i(x) == 1$
if x == 0, then $\delta_i(x) == 0$

The polynomial $f(x)$ is given as $$
\sum^{d+1}_{i=1}f(x_i) \delta_i (x)$$
$f(x_i)$ here is a value in $\mathbb{Z}_p$, NOT a function

When calculating denominator, you do the modular inverse

![[Pasted image 20250203143831.png]]

### Informal Definition
A secret $m \in \mathbb{Z}_p$ is to be shared with a threshold of t

We choose a secret degree (t-1) polynomial $f$, which satisfies $f(0) \equiv m$ (mod p)

This is like saying that the coefficient $a_0$ in our notation is exactly $m$ (mod p)

All other coefficients are chosen randomly from $mathbb{Z}_p$

The i-th user receives the point $(i, f(i)) \text{ (mod p})$ $\forall \ i > 0$

![[Pasted image 20250203145153.png]]

#### Example
![[Pasted image 20250203150523.png]]
![[Pasted image 20250203150650.png]]

### Security of Shamir secret sharing
m is an element of $\mathbb{Z}_p$, which was chosen uniformly at random

All the $a_i$ were chosen independently and randomly from $\mathbb{Z}_p$

Consider. the 'worst case' where all but a single share fall into the hans of an adversary
This means we will have:
![[Pasted image 20250203151521.png]]

This means we then have 
$$\textcolor{#ff0000}{m - y_t} \cdot r = s$$
The adversary can compute $r$ and $s$, but they cant get $m$

If $y_t$ is uniformly distributed then this is a one-time pad encryption of $m$ over $\mathbb{Z}_p$


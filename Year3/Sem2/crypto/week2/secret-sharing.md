# Secret Sharing
Our main focus will be on Boolean secret sharing and Shamir secret sharing

We want a scheme in which we can 'distribute' information about a secret to multiple parties
Only if a sufficient number of parties come together, they can reveal the secret
- If there is not enough parties, they learn nothing about the secret

![[Pasted image 20250127141222.png]]

We don't generate a key here

<span style="color:#00bfff">Share</span> takes an element and outputs a tuple of randomly selected shares
<span style="color:#00bfff">Reconstruct</span> takes a subset of $t$ or more shares as input and produces a message $m'$ as output
- We don't know if $m'$ is correct or not when it is generated

The share algorithm is probabilistic, and the output is always different
Share is a one-time thing, we need to regenerate a new one if we want to reuse it

![[Pasted image 20250127142205.png]]

There could be multiple sets of users for this

We have this weird notation for a set of authorised users because
- in real life there are complex situations
- users could be part of different organisations and need a certain number from each
- we could give some users more power than others - give the powerful user more shares

![[Pasted image 20250127142626.png]]

This is really similar to perfectly secure encryption just with shares instead of ciphertext

If an adversary can't tell the different between real shares and random output then we are cooking

![[Pasted image 20250127143800.png]]

Some resources use the term secret splitting instead of secret sharing
![[Pasted image 20250127143936.png]]

Split a message $m$ into equalish parts and assign chunks to users

This is insecure due to learning part of the secret without having $n \geq t$

### (2,2) boolean secret sharing scheme
We will assume that the purpose of the scheme is to work on bit strings
![[Pasted image 20250127144453.png]]

There are 2 sets of unauthorised users, {{1}, {2}} (no single user learns anything about $s$)
The only authorised set is {1, 2}

Correctness follows immediately from the construction

#### Security
$s_1$ is just a random string
$s_2$ is $m \oplus s_1$ - one time pad encryption of m

Since one-time pads are perfectly secret, $s_2$ is also perfectly secret

##### Formal approach
$l$ is the length of the bit string

![[Pasted image 20250127151415.png]]

$s_1$ is independent to $m$ no matter what

![[Pasted image 20250127151532.png]]

This means that all probabilities are the same, so they just look like a random bit string

![[Pasted image 20250127152024.png]]
For the right oracle, it would look exactly the same but with $m_R$ instead of $m_L$

Our goal is to find reasons to replace $m_L$ with $m_R$ so the left and right world are indistinguishable

![[Pasted image 20250127152550.png]]

since we are not returning $s_2$, it doesn't matter what we do with line 5 since it will not be returned 
However if we changed line 9, it would change what is returned

This is good for (2,n) and (n,n) schemes but not (t, n)

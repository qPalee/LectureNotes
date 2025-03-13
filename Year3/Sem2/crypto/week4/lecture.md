# Lecture

We magically assume that we can translate floating point numbers into $\mathbb{Z}_p$

Then we need to represent the function as a sequence of operations over $\mathbb{Z}_p$
- The average is a sum scaled by a constant

We express this. function as an <span style="color:#00bfff">arithmetic curcuit</span> with wires that represent values over $\mathbb{Z}_p$

![[Pasted image 20250210141531.png]]

We can scale this with more users like so
![[Pasted image 20250210141618.png]]

Computations are done through aggregation servers

Parties aren't communicating with each other, instead its with a third party entity

Multiplication by a constant is basically just distributing multiplication with each coefficient

![[Pasted image 20250210142902.png]]

The polynomial now has a much higher degree than before when doing multiplication

We have doubled out threshold

If $2t > n$ then we can no longer reconstruct the secret

From now we will assume we have enough parties to reconstruct the secret

#### Degree Reduction
This takes care of the problem of growth and the fact that we want our shares to be as random looking as possible

Each party takes their $h(i)$ and creates a new $(t, n)$ sharing for it
- Randomly divides h(i) back to new shares
- This requires everyone to do this at the same time
	- Makes it very expensive
- We give out our shares to all parties and they reconstruct using the received shares

![[Pasted image 20250210143543.png]]

Party $P_j$ computes Lagrange reconstruction with $\delta'(j)$

#### Example
![[Pasted image 20250210144902.png]]
![[Pasted image 20250210144852.png]]

### BGW
Abbreviation for Ben-Or, Goldwasser and Wigderson

The protocol provides perfect security against passive adversaries
- implies that all users behave honestly, even when taken over by an adversary

We assume that the function is given as a sequence of addition, multiplication by constant and multiplication gates

The sequence has a clear ordering which all parties know

For every multiplication gate, every party must interact

#### Protocol
##### Input Sharing
##### Computation
##### Output reconstruction

#### Security
##### Input Sharing
Perfect secrecy due to it being based on Shamir Secret Sharing
##### Computation
Each 'gate' keeps perfectly secret inputs and produces perfectly secret outputs
##### Reconstruction
With the aid of the function output, $t$ corrupt parties are unable to learn anything extra about the shares of the other parties other than the function output due to the random nature of the shares

# Verifiable Secret Sharing
There are 3 scenarios we can be in:
- **With dealer** - there is a third party which generates a secret as well as the shares and distributes the shares
- **Without dealer** - parties know their secret and want to compute something jointly based on shares
- **Implicit Secret** - shares are generated such that they define a secret without the need to construct it

#### Types of Adversaries
![[Pasted image 20250210150928.png]]

There could be multiple adversaries and they could collude

The worse case is if they collab and jointly take over $t - 1$ parties, or if they take over the dealer
- lump up the parties into a 'super adversary'
- if they have $t$ parties then we are cooked anyway since they can get the secret

#### Corrupted Dealer
With a semi-honest dealer, we can no longer hope for any secrecy in relation to the secret

If we consider a malicious adversary, it's possible that the shares are incorrect so parties cannot reconstruct the key

The best case we can hope for is that if the honest parties can identify if the dealer has been corrupt

##### Security Notion
We hope for the following properties
- **Reconstruction possible** - $t$ uncorrupted users can successfully recover the secret $s$
- **Correct secret** - if the dealer was honest, than the recovered secret is equal to the secret of the dealer
- **Share privacy** - if the dealer was honest, then $t-1$ corrupted parties learn no additional information about the secret

### Discrete Logarithm Problem
![[Pasted image 20250210151638.png]]

Sometimes this is also written as $h = \textcolor{#ff0000}{x}g$

The hardness of this problem depends on the group $\mathbb{G}$

![[Pasted image 20250210152619.png]]

The second one is basically Diffie-Hellman

If quantum computers become good then elliptic curves will be cooked
- which also means europe will be cooked

### VSS

# Cryptographic Protocols
Anyone can read the packets you send through the internet
You can't guarantee your data to stay local, it could go anywhere
We assume that the attacker has complete control of the network

## Protocol Goals
- Keys that are set up must be secret and fresh
- Both parties must authenticate
	- Both are talking to who they believe they are talking to
- Forward Secrecy
- No weak cipher
- Key Compromise Impersonation Attack
- Protocol should not be complex or have lots of different roles

### Needham-Schroeder Public Key Protocol
If Alice and Bob know each others public keys, they can set up a symmetric key

- $A \rightarrow B : E_B(N_a, A)$
- $B \rightarrow A : E_A(N_a, N_b)$
- $A \rightarrow B : E_B(N_b)$

$\textcolor{#00bfff}{E_x(\_) \text{ means public key encryption}}$

$N_a$ and $N_b$ can be used together to generate a symmetric key with xor

#### An Attack against NS
An attacker can act as a man-in-the-middle

- $A \rightarrow C : E_C(N_a, A)$
	- $C(A) \rightarrow B : E_B(N_a, A)$
	- $B \rightarrow C(A) : E_A(N_a, N_b)$
- $C \rightarrow A : E_A(N_a, N_b)$
- $A \rightarrow C : E_C(N_b)$
	- $C(A) \rightarrow B : E_B(N_b)$

##### A fix for this attack
This attack can be solved with a very simple fix:
- $A \rightarrow B : E_B(N_a, A)$
- $B \rightarrow A : E_A(N_a, N_b, \textcolor{#00ff00}{B})$
- $A \rightarrow B : E_B(N_b)$

### Forward Secrecy
A protocol has <span style="color:#00bfff">forward secrecy</span> if it keeps the message secret from an attacker who has:
- A recording of the protocol run
- The long term keys of the principals

This gives protection against a government which can force people to give up their keys or hackers that may steal them

### Diffie-Hellman
Diffie-Hellman is a widely used key agreement protocol

<span style="color:#ff0000">yap yap yap</span>

### Station-to-Station Protocol
- $A \rightarrow B : g^x$
- $B \rightarrow A : g^y, E_A(S_B(g^y, g^x))$
- $A \rightarrow B : E_B(S_A(g^y, g^x))$
- $B \rightarrow A : \{M\}_{g^{xy}}$

In this protocol, $x$, $y$ and $g^{xy}$ are not stored after the protocol run
A and B's keys don't let the attacker read M
STS has <span style="color:#00bfff">forward secrecy</span>

#### Mutual Belief
<span style="color:#ff0000">copy this slide (30) later</span>


# Cryptographic Protocols
Anyone can read the packets you send through the internet
You can't guarantee your data to stay local, it could go anywhere
We assume that the attacker has complete control of the network

## Protocol Goals
- Keys that are set up must be secret and fresh
- Both parties must authenticate
	- Both are talking to who they believe they are talking to
- Forward Secrecy

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
Diffie-Hellman is a widely used key aggreement protocol

<span style="color:#ff0000">yap yap yap</span>

### Station-to-Station Protocol
- $A \rightarrow B : g^x$
- $B \rightarrow A : g^y, \{S_B(g^y, g^x)\}_{g^{xy}}$
- $A \rightarrow B : \{S_A(g^y, g^x)\}_{g^{xy}}$
- $B \rightarrow A : \{M\}_{g^{xy}}$

In this protocol, $x$, $y$ and $g^{xy}$ are not stored after the protocol run
A and B's keys don't let the attacker read M
STS has <span style="color:#00bfff">forward secrecy</span>

#### Certificates
What if Alice and Bob don't know each other's public keys to begin with

They could meet face-to-face and set up keys, or they could get a trusted third party (TTP) to sign their identity and public key

#### Full STS Protocol
- $A \rightarrow B : g^x$
- $B \rightarrow A : g^y, Cert_B, \{S_B(g^y, g^x)\}_{g^{xy}}$
- $A \rightarrow B : Cert_A, \{S_A(g^y, g^x)\}_{g^{xy}}$

The full STS protocol adds certificates for A and B
These contain their public key signed by a TTP so Alice and Bob don't need to know each others public key


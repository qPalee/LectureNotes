3# Week 5

### The Internet
#### IP Packet header
![[Pasted image 20240506140827.png]]

#### Transmission Control Protocol
TCP is a protocol what runs on top of IP
If an IP packet gets lost, it requests for it to be resent

#### Domain Name Servers
Remembering IP addresses is hard
People created names for these instead
- news.bbc.com -> 212.58.226.141

The route for most of Europes requests is RIPE based in Amsterdam

#### The IP Stack
Internet communication uses a stack of protocols
Each protocol uses the protocol below it to send data
![[Pasted image 20240506141433.png]]

#### The attackers owns the network
- The Internet was not designed with security in mind
- Traffic may be monitored or altered
- All good security measures assume that the attacker has complete control over the network but can't break encryption

### Protocols
#### Rules
We write down protocols as a list of messages sent between <span style="color:#00bfff">principals</span>
- A -> B : "Hello"
- B -> A : "Offer"
- A -> B : "Accept"

#### A simple protocol
$A \rightarrow B : \text{"I'm Alice"}$

This message can be read by an attacker (<span style="color:#ff0000">BAD</span>)
The attacker can pretend to be anyone

$E(A) \rightarrow B : \text{"I'm Alice"}$

If Alice and Bob share a key $K_{ab}$, then Alice can encrypt her message

$A \rightarrow B : \text{\{"I'm Alice\}}_{K_{ab}}$

However an attacker can intercept and replay messages

$E(A) \rightarrow B : \text{\{"I'm Alice\}}_{K_{ab}}$

##### Nonces
A nonce is a number that is only used once, often in a challenge/response setting

- $A \rightarrow B : \text{A}$
- $B \rightarrow A : \{N_a\}_{K_{ab}}$
- $A \rightarrow B : \{N_a+1\}_{K_{ab}}, \{\text{Pay Elvis £5}\}_{K_{ab}}$

Since $N_a + 1$ was encrypted using the shared key, we can be sure Alice wants to pay Elvis £5

This protocol has a <span style="color:#ff0000">vulnerability</span> though.
![[Pasted image 20240510132431.png]]

The attacker can replay the first message sent with the encrypted nonce from the second message.

This can be fixed with a simple change though.

- $A \rightarrow B : \text{A}$
- $B \rightarrow A : \{N_a\}_{K_{ab}}$
- $A \rightarrow B : \{N_a, \text{ Pay Elvis £5}\}_{K_{ab}}$

After this protocol run Bob can be sure that:
- He is talking to Alice
- A wants to send Elvis £5
- A's messages are not replayed

#### Key Establishment Protocol
This protocol was possible because A and B share a key

Often, the principals need to set up a session key using a <span style="color:#00bfff">Key Establishment Protocol</span>

#### Needham-Schroeder Public Key Protocol
If Alice and Bob know each others public keys, they can set up a symmetric key

- $A \rightarrow B : E_B(N_a, A)$
- $B \rightarrow A : E_A(N_a, N_b)$
- $A \rightarrow B : E_B(N_b)$

$N_a$ and $N_b$ can be used together to generate a symmetric key

##### An Attack against NS
An attacker can act as a man-in-the-middle

- $A \rightarrow C : E_C(N_a, A)$
	- $C(A) \rightarrow B : E_B(N_a, A)$
	- $B \rightarrow C(A) : E_A(N_a, N_b)$
- $C \rightarrow A : E_A(N_a, N_b)$
- $A \rightarrow C : E_C(N_b)$
	- $C(A) \rightarrow B : E_B(N_b)$

###### A fix for this attack
This attack can be solved with a very simple fix:

- $A \rightarrow B : E_B(N_a, A)$
- $B \rightarrow A : E_A(N_a, N_b$, <span style="color:#00fc00">B</span>$)$
- $A \rightarrow B : E_B(N_b)$
#### Forward Secrecy
A protocol has <span style="color:#00bfff">forward secrecy</span> if it keeps the message secret from an attacker who has:
- A recording of the protocol run
- The long term keys of the principals

This gives protection against a government which can force people to give up their keys or hackers that may steal them

#### Station-to-Station Protocol
- $A \rightarrow B : g^x$
- $B \rightarrow A : g^y, \{S_B(g^y, g^x)\}_{g^{xy}}$
- $A \rightarrow B : \{S_A(g^y, g^x)\}_{g^{xy}}$
- $B \rightarrow A : \{M\}_{g^{xy}}$

In this protocol, $x$, $y$ and $g^{xy}$ are not stored after the protocol run
A and B's keys don't let the attacker read M
STS has <span style="color:#00bfff">forward secrecy</span>

### Certificates
What if Alice and Bob don't know each other's public keys to begin with

They could meet face-to-face and set up keys, or they could get a trusted third party (TTP) to sign their identity and public key

#### Full STS Protocol
- $A \rightarrow B : g^x$
- $B \rightarrow A : g^y, Cert_B, \{S_B(g^y, g^x)\}_{g^{xy}}$
- $A \rightarrow B : Cert_A, \{S_A(g^y, g^x)\}_{g^{xy}}$

The full STS protocol adds certificates for A and B
These contain their public key signed by a TTP so Alice and Bob don't need to know each others oublic key

#### Key Establishment Goals

##### Key Freshness
The key established is new - either from a TTP or uses a new nonce

##### Key Exclusivity
The key is only known to the principals in the protocol

##### Good Key
The key is both fresh and exclusive
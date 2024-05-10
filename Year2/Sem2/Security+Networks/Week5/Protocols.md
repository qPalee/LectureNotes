``# Protocols

### A simple protocol
A sends a message to B
![[Pasted image 20240212161628.png]]
This is written as A -> B: "I'm Alice"

This message can be read by an attacker
![[Pasted image 20240212161725.png]]
This is written as E(A) -> B - Elvis pretending to be Alice

![[Pasted image 20240212161821.png]]
This is written as A -> B : {"I'm Alice"}$K_{ab}$

![[Pasted image 20240212161910.png]]
Attacker can still intercept and replay messages

#### A nonce
A nonce is a number that is only used once![[Pasted image 20240212162001.png]]
![[Pasted image 20240212162107.png]]

This can still be manipulated![[Pasted image 20240212162257.png]]

There is a better method of doing it though by sending the message with the nonce, making the nonce different
![[Pasted image 20240212162322.png]]
![[Pasted image 20240212162453.png]]

### Key Establishment Protocol
- This protocol was possible because A and B shared a key
- Often, the principles need to set up a session key using a key establishment protocol
- To be sure they are communicating with the correct principal, they must either know each others public keys or use a Trusted Third Party (TTP)

![[Pasted image 20240212162717.png]]

#### An attack against the NH protocol
![[Pasted image 20240212162741.png]]
![[Pasted image 20240212162814.png]]![[Pasted image 20240212162828.png]]

This has a very simple fix by making a small change![[Pasted image 20240212162858.png]]

#### Forward secrecy
After the protocols run, the government can legally force people to hand over their private keys, whihc would allow them to read the encrypted messages
![[Pasted image 20240212163329.png]]
The protocol can be changed so that the message is secret from an attacker who has:
- A recording of the protocol run
- The long term keys of the principles

### Certificates
- What if Alice and Bob didn't know each others public keys to start off with?
- Could meet face-to-face to set up keys
- Or they could get a trusted third party to sign their identity and public key - a <span style="color:#00ff00">certificate</span>

#### Full Station-to-Station protocol
![[Pasted image 20240212163644.png]]
This adds certificates for A and B
These contain a public key certified by a TTP so Alice and Bob don't need to know each others public keys

![[Pasted image 20240212164348.png]]


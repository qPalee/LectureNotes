# Advanced Protocols

### Elliptic Curve Diffie Hellman
Elliptic curves are defined by the equation
$$\huge y^2 = x^2 + ax + b$$
A line through two points on the curve will cross one another
![[Pasted image 20241029113908.png]]

- Given 2 points on the curve, $\textcolor{#00bfff}{P}$ and $\textcolor{#00bfff}{Q}$, we find $\textcolor{#00bfff}{P+Q}$ by drawing a line through $\textcolor{#00bfff}{P \ and \ Q}$
- The other point where the line crosses the curve is $\textcolor{#00bfff}{R}$
- $\textcolor{#00bfff}{P+Q=R}$ reflected in the x axis
![[Pasted image 20241029114126.png]]

- We can take the tangent at $\textcolor{#00bfff}{P}$ to find $\textcolor{#00bfff}{P+P}$
- We can then reflect this to get $\textcolor{#00bfff}{2P}$
- We can draw a line through these to calculate $\textcolor{#00bfff}{3P}$
- This is a well defined function
	- $\textcolor{#00bfff}{p1+p2=p2+p1}$
	- $\textcolor{#00bfff}{p1+(p2+p3)=(p1+p2)+p3}$
	- $\textcolor{#00bfff}{nP+mP=(n+m)P}$

#### Making ECDH keys
- Alice and Bob agree on a curve
- They agree on a point P
	- Both the curve and P are public
- Alice picks a random $\textcolor{#00bfff}{n}$ and sends $\textcolor{#00bfff}{nP}$ to Bob
- Bob picks a random $\textcolor{#00bfff}{m}$ and sends $\textcolor{#00bfff}{mP}$ to Alice
- Alice multiplies Bob's point by her secret number
	- $\textcolor{#00bfff}{n(\text{Bob's point}) = n(mp) = nmP}$
- Bob multiplies Alice's point by his secret number
	- $\textcolor{#00bfff}{m(Alice's \ point)=m(nP)=mnP}$
- The only way that an attacker $\textcolor{#00bfff}{n}$ or $\textcolor{#00bfff}{m}$ is through brute force

These points can get very big, so we take $\textcolor{#00bfff}{mod \ p}$ of the values to limit the number of valid points
### WPA2
- WPA2 is a wi-fi security protocol developed by a closed, paid membership group of companies
- WPA2 uses AES in CCM mode
	- Security is based on a password known to the access point and client
	- This password can be brute-forced offline
![[Pasted image 20241029121447.png]]
#### Decrypting WPA
If you have the nonce, password and SSID you can get the key
- If you tell wireshark the password and SSID it will decrypt WPA traffic
- If you have $N_a, N_b, SSID$ and the encrypted message you can brute force the password offline 
### WPA3
WPA3 added the 'Dragonfly' Protocol to set up a shared secret based on the password
- Observer that knows the password cannot learn the key
- Low entropy passwords can't be brute forced
- Adds forward secrecy

After this it runs a classic 4-way handshake

WPA3 basically doing ECDH before doing WPA2
### Signal Protocol
The most secure messaging app
Its 'the best messaging app' - Tom

#### Key Derivation Function
KDF takes any input and produces a key and a key state
- Output Key is used as a session key
- Key state is used to generate more keys
![[Pasted image 20241031142644.png]]

#### Establishing a session
- Alice gets bobs keys from the server
	- Long-term, -medium term and one-time keys
- Alice generates new fresh DH key
- Alice generates the key state
...
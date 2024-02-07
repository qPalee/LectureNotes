# RSA Encryption

![[Pasted image 20240205154425.png]]

Need 2 primes p and q: p = 7, q = 11
$n = p \times q = 77$
$\phi = (p-1)(q-1) = 60$

Select a number e such that:
$1 \lt e \lt \phi \space and \space gcd(e,\phi)=1$ //e is coprime to 60
Let e = 13

Compute d such that:
$1 \lt d \lt \phi \space and \space ed \equiv 1 (mod \space \phi)$ 
Let d = 37
ed = 13x37 = 481
481 mod 60 = 1

public key:  e, N (13, 77)
private key: d, N (37, 77)

### Encrypt
Message needs to be a number between 1 and 77 but coprime to 77

$m \in \{1..77\}$
$m \notin \{7, 11, 14, 21, 22, 28, 33, 35, 42, 44, 49, 55, 56, 63, 66, 70\}$
Let m = 2

Encrypt((13, 77), 2) = $2^{13} \space mod \space 77 = 30$

### Decrypt
Decrypt((37, 77), 30) = $30^{37} \space mod \space 77 = ((2^{37}\space mod \space 77)(3^{37}\space mod \space 77)(5^{37}\space mod \space 77)) \space mod \space 77 = $

<span style="color:#00bfff">Note:</span> $x^{ab} \space mod \space n = (x^a \space mod \space n)^b \space mod \space n$











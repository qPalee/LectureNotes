# Week 4

### Public Key Cryptography

#### Secure Key Exchange
![[Pasted image 20240506135838.png]]
Remember: 
- $p$ is a large prime number
- $g < p$
- $g^a \text{ mod p}$ and $g^b \text{ mod p}$ are public keys
- $a$ and $b$ are private keys and must be primes less than p

#### RSA Encryption
![[Pasted image 20240205154425.png]]

##### RSA Keygen Example
Let $p=5$, $q=11$
$N=5 \times 11 = 55$ 
$\phi(N)=(5-1)(11-1)=40$
Suppose $e=7$, then $d=23$ since $7x23=161 \equiv 1 \text{ mod } 40$

Public Key = $(7, 55)$ 
Private Key = $(23, 55)$




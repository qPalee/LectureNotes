# Week 3

### Symmetric Cryptography

#### Modular Arithmetic
$a \space mod \space b = r \text{ for largest whole number k such that } a=b*k+r$  
$9 \space mod \space 4 = 1 \text{ because } 9=2*4+1 \text{ where } k=2$

#### xor
Xor ($\oplus$) is defined as binary addition modulo 2:
- $0 \oplus 0 = 0$
- $1 \oplus 0 = 1$
- $0 \oplus 1 = 1$
- $1 \oplus 1 = 0$

##### Important properties
- xor is associative and commutative
- for all bitstrings M, $M \oplus 0 = M$
- for all bitstrings M, $M \oplus M = 0$
where 0 is a bitstring of all 0's of the same length of M

### Advanced Encryption Standard (AES)
AES is a state-of-the-art block cipher
It works on blocks of 128 bits
It generated 10 round keys from a single 128 bit key
It uses one permutation: <span style="color:#00bfff">ShiftRows</span>, and 3 substitutions: <span style="color:#00bfff">SubBytes</span>, <span style="color:#00bfff">MixColumns</span> and <span style="color:#00bfff">AddRoundKey</span>

A block of 128 bits is represented by a 4x4 matrix where each element is a byte
![[Pasted image 20240506135041.png]]

![[Pasted image 20240506135150.png]]
![[Pasted image 20240506135204.png]]
![[Pasted image 20240506135212.png]]
![[Pasted image 20240506135231.png]]




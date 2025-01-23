# Fault Injection 1
Embedded devices, such as banking cards, the environment becomes part of adversary.

In the simplest way, you put in some data and receive encrypted data back

Fault Injection is manipulating the environment to make the processor not work as intended

The fault output leaks information about the secret data, such as a cryptographic key

#### Types of fault injection
- Power
	- Voltage Manipulation
- Clock
	- You can speed up the clock a bit to create incorrect computations
- Laser
	- You can flip a bit in RAM with a very small laser
	- Not cheap
- EM
	- Electromagnetic pulses

#### Fault Models
How can the attacker affect/change internal values
- If you have a chip what can you affect
- Specific region or just random position/width

Effects
- Bit flip
- Bits stuck at zero/one
- Statistical (chance of being flipped)
- Skip Instructions
	- Often done by changing an instruction to all 0s (nop encoding)

##### Bypassing PIN check with Fault Injection
![[Pasted image 20241118152252.png]]

###### Powerpoint tips with David
B makes the powerpoint go blank
number + enter goes to that slide

#### Generic Attack
- get fault-free ciphertext
- Inject the fault for bit 0 
	- If its unchanged, then it must be 0
	- otherwise it is 1
- Repeat for the whole number until we know the key

This is a simple attack, but effective and practical
Works in the same way for stuck-at-one faults

### Fault injection tailored to crypto algorithms
In RSA, if we inject a fault at the right time we can change a value in the algorithm which then leads to the final result to be wrong
- This has quite a large margin of error in respect to other fault injections since RSA takes a while to run

Run RSA twice, take the difference between them and do the gcd with that and n (n = p x q) and you will get q out of it.
![[Pasted image 20241121141126.png]]

As long as you don't hit both sub-exponentiatons then it will work

![[Pasted image 20241121141310.png]]

We won't have to do the calculations in the exam, we need to know the basic formulas and how they work

This fault attack don't work on regular RSA but everyone does the optimisation anyways so its fine

#### AES Fault Attacks
Given that $y=AES_k(x)$ and $y'=AES_K (X)$, we want to compute k

This attack depends heavily on the Fault Model
- random, single bit (unknown), single bit (known)

Attacker Model:
- Encrypt the same plaintext multiple times
- Toggle a bit in the last round at a known location
- ![[Pasted image 20241121142248.png]]
![[Pasted image 20241121142315.png]]

The attacker gets $y, y'$ but does NOT know $z, z'$ - but they do know the difference: $z \oplus z' =$ fault value (difference in z)
- z' is z but with 1 bit flipped

This allows us to write z in terms of the output
$y = k \oplus S(z \oplus k')$
$S(z \oplus k')=y \oplus k$
$z \oplus k' = S^{-1}(y \oplus k)$ - you can reverse s-box

We can do the same for z' but change y-> y'

We can then xor the 2 equations together
-> $S^{-1}(k \oplus y) \oplus S^{-1}(k \oplus y') = z \oplus z'$
You can then brute-force this to calculate key candidates

To brute force you have to go through all possible options for k (256 possible key bytes)
- can easily by done using a p\*thon script

This may give multiple possible key candidates
You can repeat this with a new set of y values and find out which ones remain through this

You then would need to go through the whole key byte by byte to find the whole key

##### Countermeasures
###### Detection-based
- Detect injection of fault
	- Monitor environmental conditions
- Detect faulty result
	- Compute twice and compare
- Detect 'unusual usage patterns'
###### Algorithmic
- RSA/ECC: Verify signature after signing
- AES: Backwards rounds
- Randomisation in time
	- Make it harder to inject a fault

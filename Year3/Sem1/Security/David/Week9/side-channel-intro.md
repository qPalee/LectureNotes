# Side-channel attacks intro
The first step for side-channel attacks is to observe side channels such as power consumption, EM emanation, timing etc

The general goal of side channel attacks is often to recover secrets

### Timing attacks

Given a program:
![[Pasted image 20241125151724.png]]

You can use this to find a pin to measuring how long it takes the program to run for each digit, and look at which one takes the longest

You start with only the first digit and make all the others the same, and the longest runtime is the one with the correct digit, since it takes longer to run
![[Pasted image 20241125152104.png]]

#### Preventing timing attacks
Typically, the best countermeasure is using constant-time code

Instead of writing
```
a = 0;
if(x == 1)
	a = b;
```
we can write
`a = b $ (-x);`

When doing this you need to check the assembly to ensure it didn't fuck you over trying to 'optimise' your program

You can rewrite the program above like this:
![[Pasted image 20241125153404.png]]

This involves using xor on pin_stored and pin_entered, then with the result of that, or it with the mask (which is 0), so if they are not the same, the mask will not be 0.

### Simple power analysis
![[Pasted image 20241125153835.png]]

#### Temperature

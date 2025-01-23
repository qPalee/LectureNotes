# Breaking AES

### xtime()
![[Pasted image 20241128142809.png]]
shift B by 1 to the left
If the most significant bit of B is 1
xor tmp by 0x1B
return tmp

If the runtime is longer, then we know the most significant bit is 1
We can learn the first bit of each byte with this

![[Pasted image 20241128143156.png]]

#### Outline of the attack
1. Observe program flow in power trace
2. Learn MSBit of $B_0$
3. Recovers key byte
4. Repeat for each separate byte to learn the whole key

![[Pasted image 20241128143706.png]]

Light work no reaction
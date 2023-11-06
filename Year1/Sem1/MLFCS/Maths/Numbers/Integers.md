<h1>Integers</h1>
ℕ with + and * is a commutative semiring

Z with + and * is a commutative ring

Every integer a has an additive inverse -a in Z

a + (-a) = 0

This is not the case in ℕ, since there is no negative numbers

We can deduce additive cancellation law:
	If a+x = a+y, then x=y
	Proof:
		Suppose a+x=a+y
		Then x+a = y+a
		x+(a+(-a)) = y+(a+(-a))
		x+0=y+0
		x=y
Because we've derived the additive cancellation law from the commutitive ring laws, then we know its true for any commutitive ring

We can now define subtraction
	a-b = a + (-b)

Lets prove -(-a) = a
(-a) + -(-a) = 0
(-a) + a = 0
=> -(-a) = a

[-3 .. 5) is the set of integers n such that -3 <= n < 5
-> {-3, -2, -1, 0, 1, 2, 3, 4}

[23 .. 23) has no values, the empty set

All integers can be notated as (-inf, inf)

-432 div 100 = -5
-432 mod 100 = 68

r = [0 .. 100)

-432 = 100m + r
m = -5, r=68

In Java, int uses 32 bits
Lets take 8 bits, for simplicity (Byte)
-> 0111 1111 = 127, largest  integer
Now increment
-> 1000 0000 = -128, smallest integer

The range available is [-2^7, 2^7)

In Java, the range is [-2^31 .. 2^31)
## Lists revisited

The type of lists is predefined as 
```haskell
data [a] = [] | a : [a]
```
which says that a list of a's is either empty, or else an element of type a followed by a list of a's.

This is a <span style="color:#00bfff">recursive data type</span> definition

We have the following types for the list constructors:
```haskell
[] :: [a]
(:) :: a -> [a] -> [a]
```

Although the above definitions are <span style="color:#00fc00">semantically correct</span>, they are <span style="color:#ff0000">syntactically wrong</span>

If we disregard syntax, we can define an isomorphic version as 
```haskell
Nil :: List a
Cons :: a -> list a -> List a

data List a = Nil | Cons a (List a)
```

For example, the list `[1,2,3]` is written `Cons 1 (Cons 2 (Cons 3 Nil))` in our isomorphic version of the type List.

Our isomorphic version is defined as 
```haskell
nativelist2ourlist :: [a] -> List a
nativelist2ourlist []     = Nil
nativelist2ourlist (x:xs) = Cons x (nativelist2ourlist xs)

ourlist2nativelist :: List a -> [a]
ourlist2nativelist Nil         = []
ourlist2nativelist (Cons x xs) = x:ourlist2nativelist xs
```
### Implementing operations on our list

We can implement <span style="color:#00bfff">append</span> and <span style="color:#00bfff">reverse</span> operations as
```haskell
append :: List a -> List a -> List a
append Nil         ys = ys
append (Cons x xs) ys = Cons x (append xs ys)

reverse' :: List a -> List a
reverse' Nil         = Nil
reverse' (Cons x xs) = rev xs `append` (Cons x Nil)
```
We can test this by seeing if `ourlist2nativelist (append (nativelist2ourlist xs) (nativelist2ourlist ys)) == xs ++ ys` and `ourlist2nativelist (rev (nativelist2ourlist xs)) == reverse xs` are both True $\forall$ native lists `xs, ys :: [a]`

Although the implementations of our functions are functionally correct, there is a problem with our implementation of `rev`.  Whilst `append xs ys` computes in time $O(n)$ since each call to append decreases the length of `xs` by one, `rev` does the same thing but also calls `append` which makes it $O(n^2)$ 

This is extremely obvious and a big performance issue even with reasonably large lists (length 100000).

We can define a faster reverse function by introducing a helper function with an extra argument
```haskell
fastrev :: List a -> List a
fastrev xs = revapp xs Nil
  where
    revapp :: List a -> List a -> List a
    revapp (Cons x xs) ys = revapp xs (Cons x ys)
    revapp Nil         ys = ys
```
One way to think of the `revapp` function is as a stack, initially set empty (`Nil`). The function recursively scans the input from the first argument and pushes each element onto the stack. When there are no more elements, the stack is popped to the output with the original list in reverse order

##### Illustration of fastrev
```
  fastrev (Cons 1 (Cons 2 (Cons 3 (Cons 4 Nil))))
= revapp (Cons 1 (Cons 2 (Cons 3 (Cons 4 Nil)))) Nil
= revapp (Cons 2 (Cons 3 (Cons 4 Nil))) (Cons 1 Nil)
= revapp (Cons 3 (Cons 4 Nil)) (Cons 2 (Cons 1 Nil))
= revapp (Cons 4 Nil) (Cons 3 (Cons 2 (Cons 1 Nil)))
= revapp Nil (Cons 4 (Cons 3 (Cons 2 (Cons 1 Nil))))
= Cons 4 (Cons 3 (Cons 2 (Cons 1 Nil)))
```

### An aside on accumulators 
The extra argument `ys` we used in the `revapp` function is known as an accumulator, since it accumulates a value that is eventually passed to the output. This can be used to significantly reduce the time complexity of algorithms

#### Another accumulator example
The mathematical definition of the Fibonacci Sequence can be defined as
```haskell
fib :: Int -> [Int]
fib 0 = [0]
fib 1 = [1]
fib n = fib(n-1) + fib(n-2)
```
This definition, whilst correct, is **extremely** inefficient as we are using 2 recursive calls.

We can see this by trying to compute the first 32 fibonacci numbers, which takes over 10 seconds. This is because the running time of `fib n` is ~$O(2^n)$ 

We can improve this by including accumulators `x` and `y` to our function
```haskell
fastfib :: Int -> [Int]
fastfib n = fibAcc n 0 1
	where
		fibAcc 0 x y = x
		fibAcc 1 x y = y
		fibAcc n x y = fibAcc (n-1) y (x+y)
```

With this implementation we can easily compute the first 100 numbers in a fraction of a second

To see whats going on, we can unroll the definitions as follows
```
  fastfib 7
= fibAcc 7 0 1
= fibAcc 6 1 1
= fibAcc 5 1 2
= fibAcc 4 2 3
= fibAcc 3 3 5
= fibAcc 2 5 8
= fibAcc 1 8 13
= 13

```
We can see that this function implementation of the Fibonacci numbers using a pair of accumulators is very similar to the way one might compute the Fibonacci numbers in Java, by updating variables `x` and `y` in a loop
```Java
static int fastfib(int n) {
  int x = 0, y = 1;
  while (n > 1) {
     int z = x+y;
     x = y;
     y = z;
     n = n-1;
  }
  return (n == 0 ? x : y);
}
```


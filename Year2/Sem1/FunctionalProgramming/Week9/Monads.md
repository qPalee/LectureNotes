# Monads

Monads started in Mathematics, but were first used in Programming to find side effects of functions

We want computers to be able to make changes, but Haskell was designed to not have side effects unless explicitly told to

In Haskell, there are different monads for different 'effects' you want to do.

If we have a function
```haskell
fac :: Int -> Int
```
we cannot have any side effects, as we haven't told Haskell to do so. If we wanted to print something, we have to change the type of the function to explicitly implement this.
```haskell
fac :: Int -> IO Int
fac n | n == 0 = pure 1
	  | otherwise = do
					putStrLn ("n = " ++ show n)
					y <- fac (n-1)
					pure (y*n)
```
In here, the 'do' keyword can only be used for monads

The type 'pure' is defined as
```haskell
pure :: Monad m => a -> m a
```
Which is a type cast to change an Integer into an IO Integer

To reverse this, you can use
```haskell
y <- pure 1
```
which will extract the Integer from the type IO , giving it type `Int`

The type of y in this case is 'Int'

However, the type of 
```haskell
let y = pure 1
```
will be `y :: IO Int`
### Example
We can rewrite the fibonacci function using Monads
```haskell
fib :: Monad m => Integer -> m Integer
fib 0 = pure 0
fib 1 = pure 1
fib n = do
		x <- fib (n-1)
		y <- fib (n-2)
		pure (x + y)
```
However, this is very inefficient

#### Accounting for errors using Monads
We can account for errors by using the <span style="color:#00bfff">Maybe</span> monad
```haskell
fib1 :: Integer -> Maybe Integer
fib1 n | n <  0  = Nothing
       | n == 0  = Just 0
       | n == 1  = Just 1
       | n >= 2  = case fib1 (n-2) of
                     Nothing -> Nothing
                     Just x  -> case fib1 (n-1) of
                                  Nothing -> Nothing
                                  Just y  -> Just (x+y)

```
Since fib is recursive, we are checking every time we recursively call fib1, so we can rewrite this to make it clearer
```haskell
ib1' :: Integer -> Maybe Integer
fib1' n | n <  0 = Nothing
        | n == 0 = pure 0
        | n == 1 = pure 1
        | n >= 2 = do
                     x <- fib1' (n-2)
                     y <- fib1
                     ' (n-1)
                     pure (x+y)
```
These 2 programs end up desugaring to the same code, but fib1' does error propagation for us

We can also account for errors using the <span style="color:#00bfff">list</span> monad
```haskell
fib2 :: Integer -> [Integer]
fib2 n | n <  0 = []
       | n == 0 = pure 0
       | n == 1 = pure 1
       | n >= 2 = do
                    x <- fib2 (n-2)
                    y <- fib2 (n-1)
                    pure (x+y)
```
Here we just replace `Nothing` with `[]` and `Just x` with `[x]`

This is also useful since we can then use list comprehension using this function since it returns a list

#### Printing while computing
We can use monads to 'debug' this program to see how inefficient it is

This is done using the <span style="color:#00bfff">IO</span> monad
```haskell
fib3 :: Integer -> IO Integer
fib3 n | n <  0 = error ("invalid input " ++ show n)
       | n == 0 = pure 0
       | n == 1 = pure 1
       | n >= 2 = do
                    putStrLn ("call with n = " ++ show n)
                    x <- fib3 (n-2)
                    y <- fib3 (n-1)
                    pure (x+y)
```
Calling `fib3 11` will end up printing 143 different lines, and we end up calling the same function many times, even with such a small input

##### Producing a log of computation
We can produce a log of the computation with the <span style="color:#00bfff">writer</span> monad

This is useful for when we want to know the arguments of recursive calls, but don't want to print them so we collect them into a log, which will be a list of integers. We write to the log using the <span style="color:#00bfff">tell</span> function
```haskell
fib4 :: Integer -> Writer [Integer] Integer
fib4 n | n <  0 = error ("invalid input " ++ show n)
       | n == 0 = pure 0
       | n == 1 = pure 1
       | n >= 2 = do
                    tell [n]
                    x <- fib4 (n-2)
                    y <- fib4 (n-1)
                    pure (x+y)
```

To extract the result out of an element of the writer monad, we use the function <span style="color:#00bfff">runWriter</span>
```haskell
*Main> runWriter (fib4 11)
(89,[11,9,7,5,3,2,4,2,3,2,6,4,2,3,2,5,3,2,4,2,3,2,8,6,4,2,3,2,5,3,2,4,2,3,2,7,5,3,2,4,2,3,2,6,4,2,3,2,5,3,2,4,2,3,2,10,8,6,4,2,3,2,5,3,2,4,2,3,2,7,5,3,2,4,2,3,2,6,4,2,3,2,5,3,2,4,2,3,2,9,7,5,3,2,4,2,3,2,6,4,2,3,2,5,3,2,4,2,3,2,8,6,4,2,3,2,5,3,2,4,2,3,2,7,5,3,2,4,2,3,2,6,4,2,3,2,5,3,2,4,2,3,2])
```
##### Counting the number of recursive calls
We can use the <span style="color:#00bfff">State</span> monad to count the number of recursive calls we use in our function

The <span style="color:#00bfff">state</span> monad can simulate mutable variables of the kind available in imperative languages such as C, Java and Python

In recursive calls, we modify the state by adding one to the counter `Int`

To modify the state monad, we use the <span style="color:#00bfff">modify</span> function, which is this case is `modify (+1)` which increments the state
```haskell
fib5 :: Integer -> State Int Integer
fib5 n | n <  0 = error ("invalid input " ++ show n)
       | n == 0 = pure 0
       | n == 1 = pure 1
       | n >= 2 = do
                    modify (+1)
                    x <- fib5 (n-2)
                    y <- fib5 (n-1)
                    pure (x+y)
```

We use the function <span style="color:#00bfff">runState</span> to initialise the state and run the computation
```haskell
*Main> runState (fib5 11) 0
(89,143)
```
###### Using the State monad to improve the fibonacci algorithm
We can simulate the Java method by using the <span style="color:#00bfff">state</span> monad. We use a pair `(x, y)` for the state. The return of the helper function is `()` because we only care about the state. The initial state is `(0, 1`
```haskell
fib' :: Integer -> Integer
fib' n = x`
 where
  f :: Integer -> State (Integer, Integer) ()
  f 0 = pure ()
  f n = do
         modify (\(x,y) -> (y, x+y))
         f (n-1)
  ((),(x,y)) = runState (f n) (0,1)
```
<span style="color:#00fc00">(I love this algorithm its so sexy)</span>
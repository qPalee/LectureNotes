# Definition of the Monad class
To define `Monad`, first we need to define `Definitive`, which in turn means we need to define `Functor`

```haskell
class Functor f where
fmap :: (a -> b) -> f a -> f b

class Functor f => Applicative f where
pure :: a -> f a
(<*>) :: f (a -> b) -> f a -> f b

class Applicative m => Monad m where
return :: a -> m a
(>>=) :: m a -> (a -> m b) -> m b
```
##### Functor
- Maps a function over a data structure

##### Applicative
- Assumes Functor has been defined
- Implements the pure function
	- `pure x = [x]` - List
	- `pure x = Just x` - Maybe
- <*> takes a function and an element and applies each function to each element
- List example: `<*> :: [a -> b] -> [a] -> [b]`

##### Monad
- >>= is a binding function
- Example `(>>=) :: [a] -> (a -> [b]) -> [b]`
- Return is nearly always pure, but can be other things

```haskell
g :: a -> [b]`
g x = [1..x] -- List of elements from 1 to x
xs = [10,100,1000] 
xs >>= g = [y | x <- xs,y <- g x] -- ists concat [[1..10], [1..100], [1..1000]]
```

#### Example: List
The list type former has an instance in the `Functor` class, defined as follows:
```haskell
instance Functor [] where
fmap = map
```
Map is defined in the prelude

The list type former has an instance in the `Applicative` class, defined as follows:
```haskell
instance Applicative [] where
pure x = [x]
gs <*> xs = [ g x | g <- gs, x <- xs]
```

List monad is defined as
```haskell
(>>=) :: [a] -> (a -> [b]) -> [b]
xs >>= f = [y | x <- xs, y <- f x]
```
#### Example: Maybe
The `Maybe` type has an instance in the `Functor` class defined as
```haskell
instance Functor Maybe where
fmap g Nothing  = Nothing
fmap g (Just x) = Just (g x)
```
The `Maybe` type former has an instance in the `Applicative` class, defined as follows:

```haskell
instance Applicative Maybe where
pure x = Just x
Nothing <*> xm = Nothing
Just g  <*> xm = fmap g xm
```
- If the first box has `Nothing`, then we return `Nothing`
- If not, we apply each function in the box to each element in the box

The `Maybe` monad is defined as
```haskell
(>>=) :: Maybe a -> (a -> Maybe b) -> Maybe b
Nothing >>= f = Nothing
Just x  >>= f = f x
```
#### Example: Writer
The `Writer` Monad already exists, so we will define our own version `Writer'`
```haskell
data Writer' a = Result a String
                deriving Show
                
instance Monad Writer' where
  return x = Result x ""
  xm >>= f = case xm of
               Result x s -> case f x of
                               Result y t -> Result y (s ++ t)
                               
-- Boiler plate:

instance Functor Writer' where
  fmap f xm = do x <- xm
                 pure (f x)
                 
instance Applicative Writer' where
      pure = return
      fm <*> xm = do f <- fm
                     x <- xm
                     pure (f x)

--rewrite Applicative Writer'
instance Applicative Writer' where
      pure = return
      fm >>= (\f -> xm >>= (\x -> pure (f x)))
```
This means that `(>>=) :: Writer' a -> (a -> Writer' b) -> Writer' b`

#### Example: State
The `State` monad is already defined, and so we define our own version `State'`.

The `State` monad lets us simulate variables in a storage. More abstractly, we have a state, and we can modify the state during the computation. If we are in a given state, we want to produce
- a result
- a new state

The process which does this is called a <span style="color:#00bfff">Transition function</span>, which we use `T` fro
```haskell
data State' s a = T (s -> (a,s))
```
We will use letters
- `x`, `y`, `z` for values of type `a`
- `u`,`v`,`w` for values of type `s`
- `p`,`q` for transition functions of type `s -> (a,s`

The destructor (opposite to T) is traditionally called `runState` 
```haskell
runState' :: State' s a -> (s -> (a, s))
runState' (T p) = p
```
Note that `State' s` is the monad for type `s` of states
```haskell
instance Monad (State' s) where
  return x = T (\u -> (x,u))
  -- (>>=) :: State' s a -> (a -> State' s b) -> State' s b
  xm >>= f = case xm of
               T p -> T (\u -> case p u of
                                (x, v) -> case f x of
                                            T q -> q v)
```
`return :: a -> State' s a`

The `pure` function, given a value `x`, creates a transition function that doesn't change the current state `u`, and simply pairs `x` with it.
    
The bind function `>>=` is more complicated.
    
Given `xm :: State' s a` and `f :: a -> State' s b`, we need to produce something of type `State' s b`.
We first extract the transition function from `xm` using `case` (we could have used `runState'`). This is `p`.
Then, with the constructor `T`, we create the transition function of the result `State' s a`.
Starting with the state `u`, we apply `p` to `u`.
This gives a pair, which we inspect with a `case`.
The first thing is a value `x`, which we give to `f`.
`f` produces a transition function `q`, which which we pass the state `v`.

We also need the boilerplate for the Monad
```haskell
instance Functor (State' s) where
  fmap f xm = do x <- xm
                 pure (f x)
                 
instance Applicative (State' s) where
      pure = return
      fm <*> xm = do f <- fm
                     x <- xm
                     pure (f x)
```
The above defines the monad. We also need to the define the three functions for side-effects. 
This reads the state:
```haskell
get' :: State' s s
get' = T (\s -> (s,s))
```
This replaces the state by a given state:
```haskell
put' :: s -> State' s ()
put' s = T (\_ -> ((), s))
```
And this modifies the state by applying a function to it:
```haskell
modify' :: (s -> s) -> State' s ()
modify' f = T(\s -> ((), f s))
```
## Translating do to >>=
The do notation is really just syntax sugar for >>=
For example, 
```haskell
fibm :: Monad m => Integer -> m Integer
fibm 0 = pure 0
fibm 1 = pure 1
fibm n = do
          x <- fibm (n-2)
          y <- fibm (n-1)
          pure (x+y)
```
desugars to
```haskell
fibm'' :: Monad m => Integer -> m Integer
fibm'' 0 = pure 0
fibm'' 1 = pure 1
fibm'' n = fibm'' (n-2) >>= (\x ->
           fibm'' (n-1) >>= (\y ->
           pure (x+y)))
```
We can imagine the do function as a pipeline

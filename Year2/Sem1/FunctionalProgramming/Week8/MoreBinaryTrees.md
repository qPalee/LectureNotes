# Binary Trees

Recall:
```haskell
data BT a = Empty | Fork a (BT a) (BT a) deriving (Eq, Show)
```
Recursive element where we call itself in the data type

We can make a Binary Tree by doing
```haskell
bt0 :: BT Int
bt0 = Fork 6 (Fork 7 Empty (Fork 4 Empty Empty)) (Fork 1 Empty Empty)
```

We can make a dimensional list from a Binary Tree by doing a Traversal

### In order traversal
An in-order traversal is done by going through the elements 'in order' - left to right
```haskell
inOrder :: BT a -> [a]
inOrder Empty = []
inOrder (Fork x l r) = inOrder l ++ [x] ++ inOrder r
```
This function is not unique in the sense that there are many different trees that can produce the same list

### Inverting Binary Tree traversal
There are many ways of inverting a binary tree traversal, which is also the same thing as generating a Binary Tree from a list

One way of inverting a Binary Tree traversal is by putting every element on the right node of the previous element
```haskell
invertRight :: [a] -> BT a
invertRight Empty = []
invertRight (x:xs) = Fork x (Empty) (invertRight xs) 
```

You can also invert a Binary Tree by putting every element of the left node of the previous element
```haskell
invertLeft :: [a] -> BT a
invertLeft Empty = []
invertLeft (x:xs) = Fork x (invertLeft xs) (Empty) 
```

We can create a balanced Binary Tree by doing
```haskell
invertBalanced :: [a] -> BT a
invertBalanced [] = Empty
invertBalanced xs = let (ys, z:zs) = splitAt ((length xs) `div` 2) xs
					in Fork z (invertBalanced ys) (invertBalanced zs)
```

We can give a list of all possible inversions by doing 
```haskell
invertAll :: [a] -> [BT a]
invertAll [] = [Empty]
invertAll xs = [ Fork z (l) (r) | i <- [0 .. length xs-1],
				let (yz, z:zs) = splitAt i xs,
				l <- invertAll yz, r <- invertAll zs]
```
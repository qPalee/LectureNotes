# Binary Search Trees

A binary tree is a Binary Tree in which
- Every child to the <span style="color:#00bfff">left</span> of the root is <span style="color:#00bfff">smaller</span> than the root
- Every child to the <span style="color:#00bfff">right</span> of the root is <span style="color:#00bfff">larger</span> than the root

Note that every child to the root is also a Binary Tree so the same rules apply

```haskell
isBST :: Ord a => BT a -> Bool
isBST Empty = True
isBST (Fork x l r) = x `isGT` l && x `isLT` r && isBST l && isBST r

isGT :: Ord a => a -> BT a -> Bool
isGT x Empty = True
isGT x (Fork y l r) = x > y && x `isGT` l && x `isGT` r

isLT :: Ord a => a -> BT a -> Bool
isLT x Empty = True
isLT x (Fork y l r) = x < y && x `isLT` l && x `isLT` r
```

#### Occurs
We can use a function to see if an element occurs in the BST
```haskell
occurs :: Ord a => a -> BT a -> Bool
occurs x Empty = False
occurs x (Fork y l r) | x == y = True
					  | x < y = occurs x l
					  | otherwise = occurs x r -- x > y
```
#### Insert
We can use a function to insert an element into a BST
```haskell
insert :: Ord a => a -> BT a -> BT a
insert x Empty = Fork x Empty Empty
insert x (Fork y l r) | x < y = Fork y (insert x l) r
					  | x > y = Fork y l (insert x r)
					  | otherwise = Fork y l r
					  -- When x == y, in BST elements are unique
```

#### Delete
We can use a function to delete an element from a BST
```haskell
delete :: Ord a => a -> BT a -> BT a
delete x Empty = Empty
delete x (Fork y l r) | x < y = Fork y (delete x l) r
					  | x > y = Fork y l (delete x r)
					  | x == y && l == Empty = r
					  | otherwise = let (max, rem) = popLargest l in
						  Fork max rem r
					  
popLargest :: BT a -> (a, BT a)
popLargest Empty = undefined
popLargest (Fork x l Empty) = (x, l)
popLargest (Fork x l r) = let (max, rem) = popLargest l in
							(max, Fork x l rem)
```
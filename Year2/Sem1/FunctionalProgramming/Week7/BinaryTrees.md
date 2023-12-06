# Binary Trees
A binary tree over elements of type `a` is either empty, or consists of a root labelled by an element of type `a` followed by 2 binary trees.
```haskell
data BT a = Empty | Fork a (BT a) (BT a)
```
When the tree is empty,  it is called `Empty`

Given two trees `l` and `r` and an element `x :: a`, we have the tree
```
                            x
                           / \
                          /   \
                         l     r
```
written as `Fork x l r`

##### Example
The tree 
```
                             8
                            / \
                           /   \
                          4     16
                         / \   / \
                        2        20
                       / \      /  \
```
is written as
`btexample = Fork 8 (Fork 4 (Fork 2 Empty Empty) Empty) (Fork 16 Empty (Fork 20 Empty Empty))`

### Functions on Binary Trees
#### Mirror
To start, we will make a function to mirror a Binary Tree, which when run on the tree above will give 
```
                             8
                            / \
                           /   \
                          16    4
                         / \   / \
                        20        2
                       / \       / \
```
To do this we can define the mirror function as:
```haskell
mirror :: BT a -> BT a
mirror Empty = Empty
mirror (Fork x l r) = Fork x (mirror r) (mirror l)
```
Running this on the above tree gives
`mirror btexample = Fork 8 (Fork 16 (Fork 20 Empty Empty) Empty) (Fork 4 Empty (Fork 2 Empty Empty))`

As we can see, this notation for trees is not very good to read visually but it is very good for computation
#### Size
We define the size of a Binary Tree as its total number of nodes:
```haskell
size :: BT a -> Integer
size Empty        = 0
size (Fork x l r) = 1 + size l + size r
```
We can also define the size of a BT as the number of leaves - 1:
```haskell
leaves :: BT a -> Integer
leaves Empty        = 1
leaves (Fork x l r) = leaves l + leaves r
```
#### Height
The height of a BT is defined as the longest path from the root to the lowest child, measured in number of nodes:
```haskell
height :: BT a -> Integer
height Empty        = 0
height (Fork x l r) = 1 + max (height l) (height r)
```
#### Directions, addresses and paths
To pick a subtree of a binary tree, we go left or right successively, until we find it. However a wrong list of directions may be given, so we need the `Maybe` type for the output
```haskell
data Direction = L | R deriving (Show)
type Address   = [Direction]
subtree :: Address -> BT a -> Maybe(BT a)
subtree []     t            = Just t
subtree (_:_)  Empty        = Nothing
subtree (L:ds) (Fork _ l _) = subtree ds l
subtree (R:ds) (Fork _ _ r) = subtree ds r
```
Following the above pattern, we can define a function that checks whether an address in a given tree is valid:
```haskell
isValid :: Address -> BT a -> Bool
isValid []     _            = True
isValid (_:_)  Empty        = False
isValid (L:ds) (Fork _ l _) = isValid ds l
isValid (R:ds) (Fork _ _ r) = isValid ds r
```
The list for valid addresses for subtrees can be computed as follows:
```haskell
validAddresses :: BT a -> [Address]
validAddresses Empty        = [[]]
validAddresses (Fork _ l r) = [[]]
                           ++ [L:ds | ds <- validAddresses l]
                           ++ [R:ds | ds <- validAddresses r]
```
We expect that
```haskell
    isValid ds t = ds `elem` (validAddresses t)
```
Or, in words, an address is valid if and only if it is an element of the list of valid addresses.

The list of all paths from the root to a leaf has a similar definition:
```haskell
btpaths :: BT a -> [[a]]
btpaths Empty        = [[]]
btpaths (Fork x l r) = [x:xs | xs <- btpaths l]
                    ++ [x:xs | xs <- btpaths r]
```
##### Proof on Binary Trees by induction
If we have a property `P` and we want to show that `P(t)` holds $\forall$ trees `t`, we can do this by *induction on trees* as follows:
- Argue that `P(Empty) holds`
- Argue that if`P(l)` and `P(r)` holds, then `P(Fork x l r)` also holds

### Traversals in Binary Trees
The definitions of in-order and pre-order traversals are:
```haskell
treeInOrder :: BT a -> [a]
treeInOrder Empty = []
treeInOrder (Fork x l r) = treeInOrder l ++ [x] ++ treeInOrder r

treePreOrder :: BT a -> [a]
treePreOrder Empty = []
treePreOrder (Fork x l r) = [x] ++ treePreOrder l ++ treePreOrder r
```
For instance, for the trees `btexample` and `btleft` considered above,
```
                             8
                            / \
     btexample =           /   \
                          4     16
                         / \   / \
                        2        20
                       / \      /  \
```
```
                            20
                           / \
                          16
                         / \
        btleft =        8
                       / \
                      4
                     / \
                    2
                   / \
```
we get:
```
> (treeInOrder btexample, treePreOrder btexample)
([2,4,8,16,20],[8,4,2,16,20])
> (treeInOrder btleft, treePreOrder btleft)
([2,4,8,16,20],[20,16,8,4,2])
```Breadth-First traversal is trickier. We first define a function that given a tree, produces a list of lists
```

<span style="color:#00bfff">Breadth-first traversal</span> is trickier. We first define a function that given a tree, produces a list of lists, with the nodes of level zero, , then the nodes of level 1 ... then the nodes of level n and so on.
```haskell

levels :: BT a -> [[a]]
levels Empty        = []
levels (Fork x l r) = [[x]] ++ zipappend (levels l) (levels r)
  where
    zipappend []       yss      = yss
    zipappend xss      []       = xss
    zipappend (xs:xss) (ys:yss) = (xs ++ ys) : zipappend xss yss
    ```
which gives
```haskell
> levels btexample
[[8],[4,16],[2,20]]
> levels btleft
[[20],[16],[8],[4],[2]]
```
for the above Binary Trees 

With this we can then define
```haskell
treeBreadthFirst :: BT a -> [a]
treeBreadthFirst = concat . levels
```
which concats the list of lists generated from the levels function

### Inverting traversals
Many different trees can have the same traversal, which means the functions
`treeInOrder, treePreOrder, treeBreadthFirst :: BT a -> [a]`
are non-injective and hence non-invertible.

A balanced tree can be generated from a trees in-order traversal with:
```haskell
balancedTree :: [a] -> BT a
balancedTree [] = Empty
balancedTree xs = let (ys, x:zs) = splitAt (length xs `div` 2) xs in
                  Fork x (balancedTree ys) (balancedTree zs)
```

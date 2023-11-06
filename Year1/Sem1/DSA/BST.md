Level 0 has one node, the root node

Perfect BST is a perfect triangle, every node on a level has either 2 children or no children
In a perfect BST, level n will have $2^n$ nodes

For a perfect BST of height h, it will have size $\sum^h_{n=0} 2^n$ 
S = $1+2+4+...+2^h$
2S = $2+4+8+...+2^{h+1}$
2S - S = S = $2^{h+1} - 1$                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          

To get the height from size n,
n = $2^{h+1} - 1$
$n+1 = 2^{h+1}$
$\log_2(n+1)= h+1$
$\log_2(n+1) - 1= h$
$\therefore \, h = log_2(n+1) - 1, \forall \, size \, n$

### Deleting nodes
When deleting a node, you replace it with the largest number that is smaller than the node being deleted, which will be the furthest right value on the left side of the deleted node

There are also [[AVLtrees]]







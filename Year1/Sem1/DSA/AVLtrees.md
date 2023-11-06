AVL [[BST]] are a Binary Search Tree

Height of a node is the length of the longest path from that node to a leaf node
The balance at a node is:
(Height of left subtree) - (Height of right subtree)

Height or an empty tree = -1
Balance at a leaf node = (-1) - (-1) = 0

A BST is said to be **AVL** when the balance at every node is either 1, 0 or -1

Binet's Formula:
$$F_n = \frac{\varphi^n - \phi^n}{\sqrt{5}} \approx O(1.61^k)$$
The size of an AVL tree is exponential in its height
The height of an AVL tree is logarithmic in its size
al AVL tree of size n has height O(log n)

Time complexities for BST:
- search(x) has O(log n) steps
- insert(x) we do O(1), O(log n) times -> O(log n) steps in total
- delete(x) is similar to insert, as O(log n) steps

To draw a minimal AVL of height h, you can join trees (H-1), (H-2) together with the root node


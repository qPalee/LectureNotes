A B-Tree of order m is a type of n-ary trees

Each node has at most m children
Every non-leaf node, except the root, has atleast m/2 children
The root node has atleast 2 children, if not a leaf node
A non leaf node with c children, contains c-1 search key values, which act as seperators to guide searches
All leaf nodes are in the same level
B-Trees are always heigh balanced
Update and search is O(log n)
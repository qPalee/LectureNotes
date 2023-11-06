A BHT is a complete Binary Tree which is either empty or satisfies the following conditions:
- The priority of the root $\geq$ priority of its children - the root will have the highest priority
- The left and right subtrees of the root are heap trees

Unlike in Binary Search Trees, there is no restriction on the relationship between the left and right children of any node, Binary Heap Trees do not keep the value stored in left child node  
less than that stored in the right child node.

## Insertion for BHT

Insert the value at the end of the last level and then keep bubbling it up as long as it is larger than its parent - insert at next empty location, which satisfies the CBT

As we bubble up, when we swap the value of a node with that of its parent, we don’t have to compare it with its sibling, because if the value of i is greater than that of its parent, then it must be greater than that of its sibling because of the Binary Heap Tree property.

Time compleity of O(log n)

## Deletion for BHT

- Remove the last node and use it to replace the root -> ensures CBT is satisfied
- Bubble down: Keep swapping node with the higher prioirty child 

Inseting a set of *n* items into a BHT is *n* inserts of O(log n), giving a total complexity of O(n log(n))

### Deleting an arbitrary node

The node may be anywhere in the tree
- Remove the last node and use it to replace the node being deleted
- Figure out if either bubble up or bubble down is required and do so
	Call both bubble up and bubble down, only one of these may do anything

### Updating a BHT
Change the node that needs changing then bubble up or down as nesessary
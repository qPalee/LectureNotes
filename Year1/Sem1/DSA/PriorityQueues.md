Maintains a priority list, with the highest priority item leaving first, no matter the order of input.

Highest/lowest number can be most prioritised, so they are dequeued first, making numbers in order

Obvious implementation strategies:
**Unsorted array** 
insert(x) - inserts element to the back of the queue and increment the list length O(1)
get() - search through list until highest priority element is found O(n)

**Sorted Array**
insert(x) - inserts element in correct order by searching through list O(n)
get() - take element from the end as its the highest priority element O(1)

**AVL Tree** 
Both insert and get are o(log n)

For better efficiency, you can insert the element into a **sorted array** whilst searching where to put it for O(n), but can be much shorter depending on where it must be inserted, with O(1) to get still

## Applications
Priority queues are useful whwnever we repeatedly need...

## Complete Binary Trees

A binary tree is *complete* if every level except maybe the last is completely filled, and all leaves on the last level are placed as far to the left as possible

This defines the tidiest, mos ablanced and most compact form possible for a given number of nodes. 

Eah complete Binary Tree is unique for each number of nodes, n

### Array implementation of CBT

$arr[0]$ is always empty
Root is always stored at $arr[1]$
Children of $arr[i]$: $arr[2*i]$ and $arr[2*i + 1]$
Parent of $arr[i]$: $arr[i/2]$ -> Round down bc of integer div (5.5 becomes 5)
Level of $arr[i]$: $log_2(i)$

[[BinaryHeapTrees]] are used for priority queues
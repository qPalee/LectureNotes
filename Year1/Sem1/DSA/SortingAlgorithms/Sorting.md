Given a set of records, we can sort them by many different criteria. Examples of this can be:
- Increasing/Decreasing order by number
- Alphabetic order

Sort algorithms mostly work on the basic of a comparison function which is supplied to them which defines the order required between two objects. 
In some special cases, sorting can be done without a comparison function

Java has two interfaces to implement comparison functions:
- **Comparable** - A comparable object can compare itself with another object using its compareTo() method. There is only one such method for any class
	$x.compareTo(y)$ should return a negative int, 0, or a positive int if x is less than, equal to, or greater than y respectively.
- **Comparator** - A comparator object can b used to compare ttwo objects of some type using the compare() method. This doesnt work on the current object but rather both objects passed as arguments. You can have many different functions implemented this way. 
	$compare(x, y)$ should return a negative int, 0, or a positive int if x is less than, equal to, or greater than y respectively.

## Comparison-based Sorting Strategies  
There are a number of basic strategies for comparison-based sorting, and different sorting algorithms based on each strategy:  
- **Enumeration:** For each item, count the number of items less than it, say N, then put the current item at position N + 1.  
- **Exchange:** If two items are found to be out of order, exchange them. Repeat until all items are in order.  
- **Selection:** Find the smallest item, put it in position 1, find the smallest remaining item, put it in position 2, . . .  
- **Insertion:** Take the items one at a time and insert into an initially empty data structure such that the data structure continues to be sorted at each stage.  
- **Divide and conquer:** Recursively split the problem into smaller sub-problems till you just have single items that are trivial to sort. Then put the sorted ‘parts’ back together in a  way that preserves the sorting.

## Minimum number of comparisons
For comparison-based sorting, the minimum number of comparisons necessary to sort n items gives us a lower bound on the complexity of any comparison based sorting algorithm.

Consider an array a of 3 elements: $a_0,a_1,a_2$. We can make a decision tree to figure out which order the items should be in (note: no comparisons are repeated on any path from the root to a leaf)

- This decision tree is a binary tree with one leaf for every possible ordering of the items 
- The average number of comparisons that are necessary to sort the items will be the average path length from the root to a leaf of the decision tree.  
- The worst case number of comparisons that are necessary to sort the items will be the height (h) of the decision tree.  
- Given n items, there are n ways to choose the first item, n −1 ways to choose the second, n −2 ways to choose the third, etc. so there are n(n −1)(n −2) ...3 ·2 ·1 = n! different  possible orderings of n items  
- Thus the minimum number of comparisons necessary to sort n items is the height of a binary tree with n! leaves

No comparison based sorting algorithm can have O(log n)
In the worst case, there will be a full binary tree, which will have $2^h$ leaves
Hence we need to find h such that:
- $2^h \geq n!$
- $log_2(2^h) \geq log_n(n!)$
- $h \geq log_2(n!)$

But $log_2(n!) = \theta(n log n)$, thus we need atleast *n log n* comparisons to complete a comparison based sort, which is more than log n

1There are many ways to prove this but the easiest involves showing that  
$(\frac{n}{2})^{\frac{n}{2}} \leq n! \leq n^n$ and taking the log of all terms

### Sigma Notation
When you have $\Sigma_{i=m}^{n} 1 = n-m+1$ 

## Stablility
A stable sorting algorithm does not change the order of items in the input if they have the same sort key.

Thus if we have a collection of student records which is already in order by the students’ first names, and we use a stable sorting algorithm to sort it by students’ surnames, then all students with the same surname will still be sorted by their firstnames


Bubble sort does multiple passes over an array of items, swapping neighbouring items that are out of order as it goes.

Each pass guarantees that at least one extra element ends up in its correct ordered location at the start of the array, so consecutive passes shorten to work only on the unsorted part of the array until the last pass only needs to sort the remaining two elements at the  
end of the array.

## Complexity
The outer loop is iterated (n-1) times
The inner loop is iterated (n-i) times, with each iteration executing a single comparison.
The total number of comparisons ends up as $\frac{n(n-1)}{2}$
$\therefore$ the best, worst and average comparisons are all $O(n^2)$

## Stability
Consider what happens when two elements with the same value are in the array to be sorted.  

Since only neighbouring pairs of values can be swapped, and the swap is only carried out if one is strictly less than the other, no pair of the same values will ever be swapped. Hence bubble sort can not change the relative order of two elements with the same value. 

Hence bubble sort **is stable**.
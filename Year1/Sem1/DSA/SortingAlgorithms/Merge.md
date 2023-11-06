Merge sort is a Divide and Conquer algorithm

It works by splitting the array into two halves, then using a merge sort on these new, smaller arrays recursively. It keeps splitting until each array has length 1.

It then merges the sorted parts together by comparing the smallest values from each half, then adding the smallest of the two into the sorted array. It keeps doing this until the full array is sorted

All the work is done in the merge stage, which differs from [[Quick]] Sort, in which all the work is done in the splitting stage

### Merging Efficiently
In variables i and j we store the current positions in a[-] and b[-] , res
pectively

Allocate a temporary array tmp[-] , for the result.  
2. If a[i] <= b[j] then copy a[i] to tmp[i+j] and i++ ,  
3. Otherwise, copy b[j] to tmp[i+j] and j++ .  
Repeat steps 2+3 until i or j reaches the end of a[-] or b[-], respectively, and then copy the rest from the other array.

## Complexity
Merging two arrays of lengths $n_1$ and $n_2$ is in O($n_1 + n_2)$
Each level requires O(n) for merging
If n = $2^k$ , then we have k = $log_2(n)$ levels $\implies$ O(n log n) is the time complexity of merge sort. This is true for all best, worst and average case complexity

## Stability
The splitting phase of mergesort does not change the order of any items.  

So long as merging phase merges the left with the right in that order and takes values from the leftmost sub-array before the rightmost one when values are equal, then different elements with the same values do not change their relative order.  
$\therefore$ mergesort is stable.
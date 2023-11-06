Selection sort works by selecting the smallest remaining element of the input array and appending it at the end of all the elements that have been inserted so far.  

Just like [[Insertion]] sort, it does this by partitioning the array into a sorted part at the front and an unsorted part at the end. 

Initially the sorted part is empty and the unsorted part is the whole input array.  

In each pass it finds the smallest element of the unsorted part and swaps it with the first element of the unsorted part of the array. Then it moves the split position between the sorted and the unsorted parts of the array on by one cell.

It is the same as an insertion sort however you search through the unsorted array to find the smallest element, then swap it with the first value in the unsorted list, then move the split between the two up one.

1. | 5, 12, 6, **3** , 11, 8, 4  
2. 3 | 12, 6, 5, 11, 8, **4**  
3. 3, 4 | 6, **5** , 11, 8, 12  
4. 3, 4, 5 | **6** , 11, 8, 12  
5. 3, 4, 5, 6 | 11, **8** , 12  
6. 3, 4, 5, 6, 8 | **11** , 12  
7. 3, 4, 5, 6, 8, 11 | **12**

## Complexity

The best case for selection sort is still $O(n^2)$, unlike Insertion sort, because in a selection sort, you need to still loop through the whole unsorted list no matter what to find the smallest element in the list to be able to move it, which means that it still has to do that extra loop, making it stays at $O(n^2)$. 

## Stability
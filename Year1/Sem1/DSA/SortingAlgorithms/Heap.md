Same as heapify() on an array, then bubbling down to sort

## Complexity
The heapify function is O(n).
We then have to do *n* bubble down operations, with complexity O(log n)
this gives a total complexity of O(n log n)

## Stability
Due to the reoprdering in the bubble down operations, heap sort **is unstable**
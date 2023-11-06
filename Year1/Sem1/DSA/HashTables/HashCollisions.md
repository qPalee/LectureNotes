There are two types of solutions for hash collisions:
- Chaining Strategy
	This is where each element of the hash array is a pointer of a linked list, and then you can iterate through the linked list until you find the element you want from the hash table. You also need to check if the element is already in the linked list before inserting it.
- Open Addressing strategy
	If the position of the element is already occupied, you can try a different "fallback" position. This can be done with a simple algorithm, such as n+1, 2n+1, n+3, and it will keep doing the same algorithm until an empty elemt, or the same element is found etc.
	The mod function is often used to compute fallback positions **hash(key)+1 mod T, T = arr.length}** so it loops back to the beginning on the array
	When deleting a value from the hash table, a "tombstone" is used, usually '#' so that the linear probing isn't affected

## Time Complexity

### Chaining Strategy
The worst time complexity for a hash table using the chaining strategy happens when all hash values are the same, so it is one linked list, making the time complexity will be O(n).
This can be lowered by using a good hash function

The **load factor** of a hash table is the *average* number of entries stored on a location, whihc is given by $\frac{n}{T}$, where n = total no. stored entries and T = size of hash table.

In a **good hash function**, a location given by hash(key) will be expected to have $\frac{n}{T}$ entries in that index. 
An average linear search of a linked list takes $\frac{k+1}{2}$ comparisons.
Assuming the **maximum load factor**, $\lambda$, which is $\frac{n}{T} \leq \lambda$ (In Java this is 0.75)

The average case time complexities:
- Unsuccsessful lookup: $\frac{n}{T} \leq \lambda$ comparisons $\implies$ O(1)
- Succsessful lookup: $\frac{1}{2}(1 + \frac{n}{T}) \leq \frac{1}{2}(1 + \lambda)$ comparisons $\implies$ O(1)
$\therefore \space \lambda$ is a constant number

### Linear Probing
All of the time complexities for insert(x), search(x) and delete(x) are all O(1), however there are often clusters

Primary clusters are clusters caused by entries with the same hash code. Secondary clusters are caused when the collision handling strategy causes different entries to check the same sequence of locations when they collide.  

Clusters are more likely to get bigger and bigger, even if the load factor is small. To make clustering less likely, use double hashing.

#### Double Hashing
Use primary and secondary hash functions hash1(key) and hash2(key) , respectively.  

Insertion: We try the primary position hash1(key) first and, if it fails, we try fallback positions:
$(hash1(key) + 1*hash2(key)) mod T$
$(hash1(key) + 2*hash2(key)) mod T$
$(hash1(key) + 3*hash2(key)) mod T$
...

Double hashing is an improvement of linear probing. The only difference is that every key has a different sequence of “fallback” positions given by the secondary hash function.  

Except for how we calculate the fallback positions, all the operations ( insert , delete and lookup ) work the same way; we use tombstones to mark deleted keys, when looking up we skip over those tombstones etc.

##### Short Cycles
We can have short cycles!  
A short cycle is when the double hash loops over the same values and becomes an infinite loop
Consider inserting a key such that hash1(key) = 2 and hash2(key) = 4 into a table of size 8. This will create a short cycle.

To solve this the table size, T, and hash(2) key have to be **coprime**

Two solutions:
- T is a prime number (inefficient)
- T=$2^k$ and hash2(key) is an odd number

## Full table
We say that a table is full if the load factoor is more than the maximal load factor:
$$\frac{n}{T}>\lambda$$
### Rehashing
If the table becomes full after an insertion, allocate a new table twice the size and insert all elements from the old table to it.

Consequences of insert:
- the Worst Case time complexity is O(n) during rehashing but the amorized time is O(1)

This combines well with our extra assumption that T = 2k in order to avoid short cycles. If we start from an empty hash table of such size (for example, we initially have T = 23 = 8), then doubling the size always ensures that T = 2k for some (natural) number k.

If we double the size of the hash table, we also need to change the (primary) hash function to make sure that it is good again. In practice, hash(key) is usually computed as bigHash(key) mod T (where bigHash computes a “big” hashcode).  
Then, after doubling the size of our hash table we only modify hash(key) as follows:
-bigHash(key) mod 2*T .
## Basic Idea
We would like to be able to calculate the location of our search target without having to actually search for it.

A hash function, $hash(key)$, computes the location from a key

We can have a hash table with O(1) if we have an huge array, If student number is used, it has 7 digits, so we will need an array of size $10^7$ to hold this, which is very inefficient for memory. 

Instead, we can use an array of size n mod 500, however this can cause hash collisions, in which $hash(key1) == hash(key2)$

Collisions can happen even if we double/triple the size of our array, so we need a mechanism for dealing with hash collisions

A hash table implements:
- set(key, value)
- delete(key)
- lookUpValue(key)








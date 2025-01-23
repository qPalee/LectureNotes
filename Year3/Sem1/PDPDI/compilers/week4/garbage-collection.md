# Garbage Collection
#### Problem
Efficiently manage heap-allocated memory

Two solutions:
- Manual: Leave it to the programmer
	- precise control of the memory
	- error prone
- Automatic: leave it to the runtime environment
	- programmers don't have to reclaim unused resources
	- programmers also cannot claim unused resources - wait for the garbage collector

We will assume that:
- objects have a type indicating how much memory they take up
- references to objects point to their beginning
	- cannot point to the middle of an object

Type-safe languages that cannot manipulate the memory arbitrarily are therefore good candidates for automatic GC

In unsafe languages, all memory locations can be referenced at all times

##### Performance metrics
Different metrics can be used:
- overall execution time
- space usage
- pause time

Tradeoffs must be considered when choosing what to do

#### Reachability
The set of reachable objects changes as the program executes

Termination of reachability can cause more objects to be unreachable

There are 2 basic ways to fund unreachable objects
- keep track of objects as they become unreachable (reference counting)
- periodically locate all the reachable objects
### Reference Counting
Every object stores its reference count: no. references to the object
- object allocation: reference count is set to 1
- parameter passing: reference count of each object passed into a function is incremented
- reference assignment u=v
	- increment the count for v, decrement the count for u
	- Vincent make a cool picture for this
- procedure return: all references held by local vars in the function are decremented

This is cool and all but you could also just not bother and skill issue check the user

### Mark-and-sweep
Intuition:
- stop the algorithm
- visit and mark all reachable objects
- sweep the heap to free up unreachable objects

Starts from a known set of reachable objects: the root set

The root set is the objects that can be accessed directly by a program without having to dereference pointers

Algorithm at a high level:
- input: a root set of objects, a heap, a Free list with unallocated chunks of the heap
- output: a modified Free list
- method:
	- keep track in a Unscanned list of the reachable objects, whose successors have not been checked yet.
	- once an object is reached, mark it using a reached-bit

# FloodSet Algorithm
FloodSet is an algorithm used to account for stop failures

### FloodSet for Consensus
Each process in a complete graph maintains a variable $W$ containing a subset of $V$

The $W$ belonging to process $i$ initially contains $i$'s initial value

For each of $f+1$ rounds, each process broadcasts $W$, adding all elements of the received sets to their $W$

After $f+1$ rounds, process $i$ applies a decision rule
- If $W$ is a singleton set then $i$ decides on the unique element of $W$
- Otherwise element $i$ decides on $v_0$

<span style="color:#ff0000">GO OVER THIS LATER</span>

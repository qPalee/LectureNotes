
# Bellman-Ford algorithm
Basic idea is to convert all edge-lengths to be non-negative
- make the smallest number to be 0
- doesn't work since shortest path can be changed if shortest path has more nodes visited

Assumption: there are no negative cycles
- cycles whose sum of edge lengths is negative -> no shortest path

For each vertex $v \in V$ and each $0 \leq i \leq n-1$, let
- $OPT[i, v]$ denote length of shortest $s \rightarrow v$ path having at most $i$ edges

1. If the shortest $s \rightarrow v$ path uses at most $i-1$ edges
	- The value is $OPT[i-1, v]$
2. Otherwise the last edge ($i^{th}$ edge) has to be $(w, v)$ for some $w \in V$
	- The cost of this path is $OPT[i-1, w] + cost(w, v)$
	- We need to minimise this over all $w$ such that $w, v$ is an edge in $G$

We need to minimise over both these choices

$$OPT[i, v] = min\{ \ OPT[\ i-1, v\ ]\ , \ min( \ length(w, v) + OPT[\ i-1, w \ ] \ ) \  \}$$
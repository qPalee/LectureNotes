# Greedy Algorithms

Greedy algorithms build the solution step-by-step, making local decisions to improve the solution

### Pros and Cons
#### Pros
- Very intuitive
- Easy to explain and implement
- Most heuristics are based on some greedy choices
- Sometimes can be shown to be approximately correct
#### Cons
- Many different notions of greedy
- Local 'correct' steps might not mean global correctness
- Quite often does not lead to optimal solutions
- Avoid using a greedy algorithm in practice without analysing it

### Dijkstra's Algorithm
Setting:
- A directed graph $G = (V, E)$ with $n$ vertices
- Edge-lengths given by $length : E \rightarrow R^{\leq 0}$
- A fixed source vertex $s$
- For each $v \in V$, find length of shortest path $s \rightarrow v$ path

For this we need to find $n$ values

1. Let $S$ be set of explored vertices
2. For each $u \in S$ we store distance of shortest $u \rightarrow s$ path in $dist(u)$
3. Initialise $S = \{s\}$ and $dist(s) = 0$
4. **while** $S \neq V$ **do**
5.      Select a vertex $v \not\in S$ which minimises $temp-dist(v) = min(dist(u) + length (u, v))$ where $(u, v) \in E, u \in S$
6.      Add $v$ to $S$ and set $dist(v) = temp-dist(v)$
7. end **while**


#### Time Complexity
Running time is $O(nm)$ where $n, m$ is number of vertices, edges respectively

We run the while loop $n-1$ times from size of $|S|=1$ to $|S|=n$
In each instance of the while loop, we need to check every edge, which gives us $m$ computations per loop

#### Correctness of Dijkstra's algorithm

>[!info] Theorem
>Consider the set $S$ at any point during the algorithm. For each $u \in S$, the quantity $dist(u)$ stores the value of shortest $s \rightarrow u$ path


We prove this theorem by induction on $|S|$:
- Base case: $|S|=1$ and $dist(s)=0$
- Inductive Hypothesis: Suppose the theorem holds for $|S| = k$
- Suppose that we now grow $S$ by one more vertex by adding $v$
- We know that $temp-dist(v) = dist(u) + length(u, v)$ for some $u \in S$
- Suppose there is a $s \to v$ path $P$ shorter than $dist(v)$
- Let this path $P$ leave $S$ via the edge $(x, y)$ for some $x \in S, y \not\in S$
- This is a contradiction

tldr: cant be a shorter path since if there was Dijkstra would've chosen it


also look at negative edge weights and how it cooks this proof

# Minimum Spanning Trees

Let $G= (V, E)$ be an undirected, connected graph with $n$ vertices
- connected $\rightarrow$ there is a path between any two vertices

A subgraph $T=(V', E')$ of $G$ is said to be a spanning tree of $G$ if:
- $V' = V$ $\rightarrow$ <span style="color:#00bfff">spanning property</span>
- $|E'| = n-1$ $\rightarrow$ <span style="color:#00bfff">tree property</span>

A spanning tree has $n$ vertices and $n-1$ edges

>[!info] Minimum Spanning Tree problem
>Given an undirected, connected graph $G=(V, E)$ with edge-costs given by $cost: E \rightarrow \mathbb{R}^{+}$, find a spanning tree $T=(V, E')$ such that $\Sigma_{e \in E'} cost(e)$ is minimised

### Prim's Algorithm

1. Let $S$ be set of explored vertices
2. Initialise $S = \{ s \}$ where $s$ is any vertex
3. Initialise $E' = \emptyset$
4. **while** $s \neq V$ **do**
5.      Select a vertex $v \not\in S$ which minimises $min(cost(e)), e = u-v, u \in S$
6.      Add $v$ to $S$ and $e$ to $E'$
7. **end while**

#### Complexity of Prim's Algorithm
While loop has $n$ iterations $\rightarrow |S| = 1$ to $|S| = n$
In each loop, you need to check every edge leaving edge on that node which is $\geq |E| = m$

#### Correctness of Prim's Algorithm
Assumption: All edge-costs are distinct

>[!info] Theorem
>For any $S \subset V$ let $e$ be the edge of minimum cost having one end-point in $S$ and other end-point in $V \backslash S$ Then every MST contains the edge $e$

- Suppose there is a MST $T$ which does not contain the edge $e$ whose endpoints are $u \in S$ and $w \not\in S$
- We will find an edge $e' \in T$ such that $cost(e') > cost(e)$
- If we replace $e'$ with $e$ we get a spanning tree with a smaller cost. <span style="color:#ff0000">Contradiction</span> 

### Kruskal's Algorithm

1. Order edges of $E$ as $e_1, e_2, ..., e_m$ in increasing order of costs
2. Initialise $E' = \emptyset$ and $i=1$
3. **while** $i \leq m$ **do**
4.      if adding $e_i$ to $E'$ doesn't create a cycle
5.           Add $e_i$ to $E'$
6.      increment $i$
7. **end while**

#### Complexity of Kruskal's Algorithm
Running time is $O(nm)$ where $n, m$ is the number of vertices, edges respectively

While loop runs $n$ times -> $n$ vertices
Inside each loop we need to check if adding edge creates a cycle -> $m$

#### Correctness of Kruskal's Algorithm
Assumption: Add edge-costs are distinct

>[!info] Theorem
>For any $S \subset V$ let $e$ be the edge of minimum cost having one end-point in $S$ and other end-point in $V \backslash S$ Then every MST contains the edge $e$


- Suppose the edge $v-w$ gets added at this step
- Let $S$ be set of all vertices to which $v$ had a path before this step
- Clearly $w \not\in S$
- Before this step, no edges from $S$ to $V \backslash S$ have been added
- Since $v \in S$ and $w \not\in S$ it follows that $v-w$ is the cheapest edge with one end-point in $S$ and the other end-point in $V \backslash S$

# Interval Scheduling
Setting:
- We are given a set of $n$ requests $R=\{Req(1), Req(2), ..., Req(n)\}$
- $Req(i)$ has a start time given by $Start(i)$ and finish time given by $Finish(i)$
- There is a machine which can handle one request at a time
- Two requests "conflict" if they overlap

>[!info] The $INTERVAL SCHEDULING$ problem
>Select a set $C \subseteq R$ of requests such that $|C|$ is maximised and no two requests from $C$ conflict

<span style="color:#00bfff">type ts out later</span>

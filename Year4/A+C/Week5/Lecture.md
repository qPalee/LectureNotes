# MergeSort

Given a list of $n$ numbers, we want to sort them in increasing order:
- Divide the problem into smaller parts
- Why not two parts, and roughly equal parts?

Say we have a list $\{1, 5, 3, 4, 6, 7, 0 \}$

First step is to divide:
$\{1, 5, 3, 4 \}$ and $\{6, 7, 0 \}$

Then we conquer:
We need to solve both smaller lists
$\{1, 3, 4, 5 \}$ and $\{0, 6, 7\}$

Finally we need to combine:

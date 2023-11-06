We can multiply a matrix by a scalar, r $\forall \, r \in \mathbb{Q}$ 
$$3\begin{pmatrix} a_1 & a_2 \\ b_1 & b_2 \end{pmatrix} = \begin{pmatrix} 3a_1 & 3a_2 \\ 3b_1 & 3b_2 \end{pmatrix}$$

We can also multiply matrices:

Let A be a m x n matrix with row i and column j given by $a_{ij}$
Let B be a n x p matrix with row j and column k given by $a_{jk}$

A x B will be an (m x p) matrix C whose entry $C_{ik}$ is given by:
$$C_{ik} = \sum_{j=1}^{n} a_{ij} \text{ x } b_{jk} = (a_{i1} \text{ x } b_{1k}) + (a_{i2} \text{ x } b_{2k}) + .... + (a_{in} \text{ x } b_{nk})$$
#### Example
$A = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix} \, B = \begin{pmatrix} 7 & 8 \\ 9 & 10 \\ 11 & 12 \end{pmatrix}$ 

$$AB = \begin{pmatrix} (1 \times 7) + (2 \times 9) + (3 \times 11) & (4\times 7) + (5 \times 9) + (6 \times 11)\\ (1 \times 8) + (2 \times 10) + (3 \times 12) & (4 \times 8) + (5 \times 10) + (6 \times 12)\end{pmatrix} = \begin{pmatrix} 33 & 139\\ 64 & 154\end{pmatrix}$$
### Associativity and Commutativity
Matrix multiplication is not commutative
$\implies$ AB $\neq$ BA

However it is associative
$\implies$ A(BC) = (AB)C
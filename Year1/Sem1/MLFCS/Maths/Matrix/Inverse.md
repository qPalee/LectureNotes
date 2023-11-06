To find the inverse of a matrix we first need to know the [[Identity]] Matrix

The inverse of a Matrix is defined to be Matrix B such that $BA = I$
To find the inverse, we must find matrix B that multiplies with A to create the Indentity Matrix
$$\begin{pmatrix} r & s \\ x & y \end{pmatrix} \cdot \begin{pmatrix} 1 & 2 \\ 3 & 8 \end {pmatrix} = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$$
$$\begin{pmatrix} r + 3s & 2r + 8s \\ x + 3y & 2x + 8y \end{pmatrix} = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$$
$\therefore r + 3s = 1, 2r + 8s = 0, x + 3y = 0, 2x + 8y = 1$
Now we have 2 sets of linear equations that can be solved to give us matrix B

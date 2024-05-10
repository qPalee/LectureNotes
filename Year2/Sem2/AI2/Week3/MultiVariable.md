# Measures for more variables

<span style="color:#ff0000">Need to know how to construct a PMF table</span>
### Joint Entropy
"A measure of the uncertainty associated with a set of variables.”.

For two discrete random variables X and Y, the joint entropy is defined as: $$H(X,Y) = -E[log_p (X,Y)] = - \sum_{x_i \in R_X} \sum_{y_j \in R_Y} p(x_i, j_i) \space log_p(x_i, y_i)$$
The Joint Entropy equation is heavily linked with the PMF table

### Conditional Entropy
Conditional Entropy quantifies uncertainty of the outcome of a random variable  $Y$ given the outcome f another random variable $X$, which is defined as:
$$H(Y|X)=-E[log_p(Y|X)]=-\sum_{x_i \in R_X} \sum_{y_j \in R_y} p(x_i, y_j) \space log_p (y_j|x_i)$$
Conditional Entropy can also be derived from this Venn Diagram:
![[Pasted image 20240202102715.png]]

### Mutual Information
Mutual Information measures the information that X and Y share
Intuitively, it measures how much knowing one of these variables reduces uncertainty about the other
Formally, the mutual information of 2 discrete random variables X and Y is defined as $$I(X;Y)=\sum_{x \in R_x} \sum_{y \in R_y} p(x,y) \space log(\frac{p(x,y)}{p(x) \space p(y)})$$
#### Mutual Information and Entropy
We can also express mutual information in terms of joint and conditional entropies:
$I(X;Y)\equiv H(X)-H(X|Y)$ 
			$\equiv H(Y)-H(Y|X)$
			$\equiv H(X) + H(Y) - H(X,Y)$
			$\equiv H(X,Y)-H(Y|X) -H(X|Y)$

![[Pasted image 20240202103616.png]]
#### Properties of Mutual Information
- Non-negativity: $I(X;Y) \geq 0$
- Symmetric: $I(X;Y) = I(Y;X)$
- Measure of dependence between X and Y:
	- $I(X;Y)=0 \iff X \bot Y$
	- $I(X;Y)$ increases with $H(X)$ and $H(Y)$ as well as dependence of X and Y
- $I(X;X)=H(X)-H(X|X)=0$


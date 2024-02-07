# Measures for more variables

<span style="color:#00bfff">Need to know how to construct a PMF table</span>
### Joint Entropy
"A measure of the uncertainty associated with a set of variables.”.

For two discrete random variables X and Y , the joint entropy is defined as: $$H(X,Y) = -E[log_p (X,Y)] = - \sum_{x_i \in R_X} \sum_{y_j \in R_Y} p(x_i, j_i) \space log_p(x_i, y_i)$$
The Joint Entropy equation is heavily linked with the PMF table

### Conditional Entropy
![[Pasted image 20240202102715.png]]

### Mutual Information
Mutual Information measures the information that X and Y share
Intuitively, it measures how much knowing one of these variables reduces uncertainty about the other
Formally, the mutual information of 2 discrete random variables X and Y is defined as $$I(X;Y)=\sum_{x \in R_x} \sum_{y \in R_y} p(x,y) \space log(\frac{p(x,y)}{p(x) \space p(y)})$$
#### Expressing Mutual Information in terms of joint and conditional entropies
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


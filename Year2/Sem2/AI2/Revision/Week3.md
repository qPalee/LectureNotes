# Week 3

### Joint Entropy
Joint Entropy is a measure of the uncertainty associated with a set of variables.

For two discrete random variables $X$ and $Y$, the joint entropy is defined as:
$$H(X,Y)=-\sum_{x_i \in R_X} \sum_{y_i \in R_Y} P(x_i, y_i)\space log(x_i, y_i)$$
### Conditional Entropy
Conditional Entropy quantifies uncertainty of the outcome of a random variable $Y$ given the outcome of another random variable $X$

We can define Condition Entropy as 
$$H(Y|X)= -\sum_{X_i \in R_X} \sum_{X_j \in R_Y} p(x_iy_i)log_p(y_i | x_i)$$

#### Chain Rule for Conditional Entropy
We can use the chain rule and the condition probability $p(y|x)=\frac{p(x,y)}{p(x)}$ to rewrite Conditional Entropy as:
$$H(Y|X)=H(X,Y) - H(X)$$
![[Pasted image 20240502161131.png]]

### Mutual Information
Mutual Information measures the information that $X$ and $Y$ share. More specifically it <span style="color:#00bfff">measures how much knowing about one variables reduces uncertainty about the other</span>.

The mutual information between 2 discrete random variables $X$ and $Y$ can be defined as:
$$I(X;Y)=\sum_{X \in R_X} \sum_{Y \in R_Y} p(x,y) \space log(\frac{p(x,y)}{p(x) \space p(y)})$$
#### Entropy
We can express Mutual Information in terms of join and conditional entropy
![[Pasted image 20240502161604.png]]

#### Properties of Mutual Information

##### Must be positive
$I(X;Y) \geq 0$

##### It is symmetric
$I(X;Y) = I(Y:X)$ 

##### If 2 variables are equal their Mutual Information is 0


![[Pasted image 20240502163442.png]]

![[IMG_0062.jpeg]]![[IMG_0063.jpeg]]


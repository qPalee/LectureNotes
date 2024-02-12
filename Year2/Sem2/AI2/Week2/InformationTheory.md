# Information Theory
An event contains more information if it is less probable/more surprising
If two independent events are measured separately, the total amount of info is the sum of the self informations of the individual events

### Self Information
Given a random variable X with probability mass function $P_X(x)$, the self information of meauring X as outcome x is defined as $$I_X(x)=log_b [P_X(x)]=log_b \frac{1}{P_X(x)}$$
where different bases of the logarithm b results in different units:
- b=2 : bits
- b=e : 'natural units'
- b=10 : 'dits', 'bans', 'hartleys'

### log-odds
Given some event $X$, and $p(X)$ is the probability of x occurring, and that $p(\neg x)=1-p(x)$ is the probability of $X$ not occurring. From the definition of logit:
$$\text{logit}=log(\frac{p}{1-p})=log(p)-log(1-p)$$
we can derive:
$$logit(X) = I(\neg X) - I(X)$$

### Entropy
Entropy quantifies the uncertainty in a random variable $X$. 
More formally, given a discrete random variable $X$ with range $R_X = \{X_1,...,X_n\}$, and its probability mass function as $P_X(X)$, the entropy of X is formally defined as 
![[Pasted image 20240212143456.png]]

#### Example 1: Fair and biased coins
Denoting the outcome of tossing a fair coin or a biased coin as $X$ and $Y$ respectiverly. We know the biased coin has a probability of landing on heads of 0.7. Calculate their entropies and interpret the results.

$$H(X)=-\sum^{n}_{i=1}P(X_i) \space log_2 P(X_i)=-\sum^{2}_{i=1}\frac{1}{2}log_2\frac{1}{2}=-\sum^2_{i=1}\frac{1}{2} \cdot (-1) = 1$$
$$H(Y)=\sum^{n}_{i=1}P(X_i) \space log_2 P(X_i)=-0.7\space log_2(0.7) \space - \space 0.3 \space log_2(0.3) \approx 0.8816$$

#### Example 2: Quantifying the information of English
Regarding the English language as a discrete random variable $X$ with the range $R_X=\{1,2,3,...,27\}$, in which the values 1-26 represent the 26 letters (a-z) and 27 represents the space character.

##### Step 1
To obtain the PMF of $X$, we choose a book "The frequently Asked Questions Manual for Linux" and calculate the experimental probabilities of the 27 characters (shown below)

##### Step 2
Calculate the entropy
$$H(X)=-\sum^n_{i=1}P(X_i) \space log_2 P(X_i)=4.11 (\text{bits/letter})$$
![[Pasted image 20240212144620.png]]

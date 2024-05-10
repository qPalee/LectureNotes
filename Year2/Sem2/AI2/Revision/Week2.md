# Week 2

### Odds
Odds describes the probability of a <span style="color:#00bfff">binary outcome</span> 
$$odds=\frac{p}{1-p}$$

### Logit
Logit, or log-odds, is just the logarithm of the odds
$$logit(p)=log(\frac{p}{1-p}) = log(p)-log(1-p)=-log(\frac{1}{p}-1)$$
### Calculating probability from odds
$$p=\frac{1}{1+\frac{1}{odds}}$$
### Logistic regression
A logistic model can be formally defined as:
$$logit = log(\frac{p}{1-p})=\theta_0 + \theta_1 x_1 + \theta_2 x_2 + ... + \theta_n x_n$$

#### Assumptions

##### Binary outcomes

##### Independent observations 
Observations are independent of each other - they should not come from repeated measurements or matched data
##### Low or no multicollinearity among the independent variable
The independent variables are not too highly correlated with each other
##### Linearity of independent variables and log odd
This does not mean logistic regression assumes the dependent and independent variables are related linearly
##### A large sample size
<span style="color:#00bfff">Rule of ten:</span> to fit a logistic regression model, we need at least 10 cases with the least frequent outcome for each independent variable in your model. For example, if you have 5 independent variables and the expected probability of your least frequent outcome is .10, then you would need a minimum sample size of 10x5 / .1 = 500

### Self Information
Given a random variable X with probability mass function $P_X(X)$ , the self-information of measuring X as outcome x is defined as
$$I_X(X)=-log_b[P_X(x)]=log_b(\frac{1}{P_X(x)})$$
Where different bases of the logarithm function $b$ result in different units:
- b=2: bits
- b=e: natural units
- b=10: hartleys

#### Logit
Logit also links in with Self information with the formula:
$$logit(x)=I(\neg X)-I(X)$$
### Entropy
Entropy quantifies the uncertainty in a random variable X

Given a <span style="color:#00bfff">discrete random variable</span> X with probability mass function $P_X(X)$, the entropy of X is defined as:
$$H(X)=-\sum^n_i P(X=x_i) log_b P(X=x_i)$$
#### Example
Denoting the outcome of tossing a fair coin or a biased coin as X and Y , respectively. We know the biased coin comes up heads with probability of 0.7. Calculate their entropies and interpret the results 

![[Pasted image 20240502134919.png]]

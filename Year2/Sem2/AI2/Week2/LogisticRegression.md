# Logistic Regression

Logistic Regression is a regression model where the prediction is <span style="color:#00bfff">binary</span>
- The goal is to predict the probability that a given example belongs to the '1' class versus the probability that it belongs to the '0' class
- Done using either the <span style="color:#00bfff">logarithm of the odds</span> or the <span style="color:#00bfff">logistic function</span>

Logistic regression is still very useful, even when a simple version is used

A logistic regression can also be seen as a simple neural network with no hidden layers

### Odd ratio vs Probability
##### Probability
Probability is a number $p \in [0,1]$ between 0 to 1 to describe how likely an event is to occur, or how likely it is that a proposition is true, assuming we know the distribution of the data 

##### Odds
A number to describe the probability of a <span style="color:#00bfff">binary outcome</span>, which is either present or absent, such as mortality. Specifically, the odds are the ratio of the probability that an outcome present, such as $p$ to the probability that the outcome absent, such as $1-p$
$$\text{odds}=\frac{p}{1-p}$$

###### Logit: the logarithm of the odds:
$$\text{logit}(p)=\text{log}(\frac{p}{1-p})=\text{log}(p)-\text{log}(1-p)=-\text{log}(\frac{1}{p}-1)$$
#### Example
Assume we have a deck of 52 cards

What is the <span style="color:#00fc00">probability</span> of drawing a card randomly from the deck?
- the probability of randomly drawing a card from the deck and getting spades is $\frac{13}{52}$

What are the <span style="color:#00fc00">odds</span> of drawing a spade?
- Since the probability of not drawing a spade is $1-\frac{1}{4}$, the odds are $\frac{1}{4} : \frac{3}{4}$, or $1:3$ 

### Assumptions of Logistic Regression
- Binary Outcomes
- Independent observations - shouldn't come from repeated measurements
- Low or no <span style="color:#00fc00">multicollinearity</span> among independent variables - variables are too highly correlated
- Linearity of independent variables + log odds
- A large sample size - need at least 10 cases with the least frequent outcome for each independent variable

### Using logistic regression
Results interpretation:
- Model intercept - $\theta_0: -1.2725$
- Model coefficients - $\theta_1 : 0.2064$

From the results we can calculate:
- Odds:
$$\text{odds}=\frac{p}{1-p}=\text{exp}(\theta_0 + \theta_1 X_1)=\text{exp}(-1.2725+0.2064 \space X_1=\text{exp}(0.2064 \cdot (-6.1652 + X_1))$$
- Probability: (Note: $p=\frac{1}{1+\frac{1}{\text{odds}}}$)
$$P(Y=1)=\frac{1}{1+\text{exp}(-(\theta_0 + \theta_1 X_1))}=\frac{1}{1+\text{exp}(-0.2064 \cdot (-6.1652+X_1))}$$

The model intercept is the log-odds of the event that you pass the exam when you spend 0 hours revising.


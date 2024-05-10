# Maximum Likelihood Estimation

Maximum likelihood estimation searches the best parameters of a probability distribution that makes the data most likely

#### Intuition
##### Input: 
Observations (real data points)  
##### Output: 
A model that can generate synthetic data that is most similar to the observation  
##### Model: 
Probability distribution  
##### Task: 
Search for the best parameters of the model (probability distribution) to fit the observations

### Maximim Likelihood Estimator (MLE)
![[Pasted image 20240212131134.png]]

<span style="color:#00fc00">^^IMPORTANT PARTS^^</span>
### Difference between probability and likelihood

##### Probability
Probability is a number $p \in [0,1]$ between 0 to 1 to describe how likely an event is to occur, or how likely it is that a proposition is true, assuming we know the distribution of the data 

##### Likelihood
Likelihood is a function which measures the goodness of fit of a statistical model to a sample of data for given values of the unknown parameters, such as $\theta$ 

Essentially likelihood is needed when there are unknown parameters

### How to solve optimisation problems
#### Option 1
Exhaustive Search
- Only works for low dimensional problems

#### Option 2
Grid Search
- Used for tuning hyper-parameters of a machine learning model

#### Option 3
Optimisation algorithms

### Cost Function
A function that maps a set of events into a number that represents the 'cost' of that event occurring.
Also known as the <span style="color:#00bfff">loss function</span> or <span style="color:#00bfff">objective function</span>.

#### Cost Function for likelihood
A general one-to-one mapping with likelihood - the negative logarithm of the likelihood function:
$$J(\theta, D)=-log(L(\theta \space | \space D))$$
##### Why use the negative log of likelihood function?
<span style="color:#00bfff">Convention:</span>
- By convention, many optimisation problems are minimisation problems

<span style="color:#00bfff">Convenience:</span>
- Taking the logarithm changes multiplication to addition -- $log(AB) = log(A) + log(B)$ -- which is easier to differentiate

<span style="color:#00bfff">Numerically stable:</span>
- Product of $\theta$, which is a probability will converge quickly to zero, which might cause problems for computers who are limited by machine precision
- 
![[Pasted image 20240212132914.png]]


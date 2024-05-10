# Theory Application to Machine Learning

### Decision Trees
<span style="color:#ff0000">NOT IN EXAM but useful to learn</span>
Decision Trees are one of the most popular Machine Learning algorithms because of their:
- Simplicity
- Interpretability
- Extendability
##### Applications
- Decision Trees for Credit Card fraud detection
- Customer Service Automation
- AI Reveals the perfect pancake recipe

#### Information gain for Decision Trees
It is the information we gain after spiting the samples based on an independent variable
Formally, information gain is defined as the change in information entropy H from a prior state to a state that takes some information as given: $$IG(Y,X)=H(Y)-H(Y|X)$$
where Y is a random variable that represents the dependent variable and X is one of the independent variables, and $H(Y|X)$ is the conditional entropy of Y given X

<span style="color:#00bfff">Information gain actually is Mutual Information</span>
$I(X;Y)\equiv H(X)-H(X|Y)$
			$\equiv H(Y)-H(Y|X)$

##### Mutual Information feature selection
Use mutual information to choose an optimal set of independent variables, called features that allow us to classify samples. Formally, given an initial set $F$ with $n$ independent variables, **X**=$\{X_1, X_2,...,X_n\}$, find subset with $S \subset F$ features that maximises the Mutual Information $I(Y;S)$ between the dependant variable $Y$ and the subset of selected features $S$

![[Pasted image 20240202112011.png]]
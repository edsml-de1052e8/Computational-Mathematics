## Lecture 6: Probability


-> see class notes

**Machine Learning**

- Labelled data is data that was previously annotated (most likely by a human) to show the expected result of running the model/algorithm, e.g. an image of a cat, accompanied by metadata that identifies it as a cat.
- Unlabelled data is data without annotations, e.g. an image of a cat without any additional information to help us identify it as a cat.

- Supervised learning uses labelled data to train an algorithm to reproduce the task that the labelled data serves as examples of.
- Unsupervised learning uses unlabelled data to extract natural patterns from data, e.g. clusters of similar data points.
- Semi-supervised learning uses both labelled and unlabelled data in order to try to achieve the best of both previous approaches.


**Supervised learning**

- Regression: random variable is continuous
- Classification: random variable is discrete

- Linear Regression represents the simplest machine learning algorithm for a regression task, but there are many more. 

- Bayes Theorem: ayes’ Theorem uses the sum rule and the product rule.
he product rule tells us that:

P(Y=y \, | \, X=x) = \frac{P(X=x, Y=y)}{P(X=x)}
\qquad (2)

Similarly, the product rule tells us that the reverse probability of $X=x$, given that $Y=y$ is expressed as:


P(X=x \, | \, Y=y) = \frac{P(Y=y, X=x)}{P(Y=y)}

which can also be written as follows:


P(Y=y ,X=x) = P(X=x \, | \, Y=y)P(Y=y)
\qquad (3)$$
In addition, note that the probability of getting $X=x$ and $Y=y$ ($P(X=x ,Y=y)$) is equivalent to the probability of getting $Y=y$ and $X=x$ ($P(Y=y ,X=x)$):


P(Y=y, X=x) = P(X=x, Y=y)

- In terms of classification

- P(Y) is the prior probability of the class $Y$.
- P(X)$ is the prior probability of the predictor $X$.
- P(X|Y)$ is the likelihood, or the probability of the predictor given the class. 
- P(Y|X)$ is the posterior probability of the class $Y$, given the predictor $X$. This is the most interesting quantity here and the one we are most likely interested in calculating.


**Naive Bayes Classifier**


- The word naive in the name points at our clearly naive assumption of the independence of features.

From Bayes theorem, to calculate $P(Y|X)$, we need $P(X|Y)$, $P(Y)$, and $P(X)$:

$$
P(Y=y \, | \, X=x) = \frac{P(X=x \, | \, Y=y) P(Y=y)}{P(X=x)}
$$
$P(Y)$ is the prior probability of class $Y$ - i.e. the probability of the data belonging to a particular class before we've seen $X$.

Since our dataset contains 50 data points for each of the three classes, the prior probabilities of all three classes is $P(Y)=\frac{1}{3}$.

$P(X)$ is the probability of observing the data value(s) $X$, regardless of the class (i.e. using the distribution for all data),

while $P(X|Y)$ is the probability of observing the data value(s) $X$, given that the class is $Y$ (i.e. using the distribution for the data for a particular class).

In python this calculate probability for each class Y
P(Y|X)=P(X|Y) x P(Y)/P(X) - returns the probabilities for each class Y
NB: data_prior is P(X)


**Accuracy**

- Defined as the ratio of correct predictions with total number of predictions for the classifier
- However, there is something VERY WRONG about using the same data for both model training and for testing/inference...

- We are using the same data to train the model and then test it - this is like giving a student the model answers during an exam. 
- The correct way would be to split our data into training and testing sets, where we use the training dataset to train our model, and then the test dataset to evaluate its performance.

**Likelihood**

- Expresses uncertainty about distribution of data rather than data itself.
- The likelihood can be defined as the function of Lx (theta) = P(x|theta) where $\theta$ are **parameters** describing the probability distribution function. 
- It represents the likelihood of observing the data $\mathbf{x}$ for the random variable $X$ given the model parameters.
- log of products is sum of multipliying logs -> trying to maximise likelihood, same as minimising the negative log likelihood (feed into optimisation)
- Maximum likelihood estimation: calculate the likelihood of observing the data we have ($\mathbf{x}$), for different values of the model parameters ($\theta$), choosing the value of $\theta$ that maximises $L_x(\theta)$

NB: P (theta|x) is said 'probability of theta given x. 

- Maximum a posteriori estimation: trying to find the theta that maximises arg max theta P(theta|x). 

- Linear regression:  fitting a straight line to data points
y= Beta0 + Beta1x

Some assumptions for linear regression: 
- The residuals are all independent 
- The residuals are identically distributed, i.e. they are all drawn from the same distribution (e.g. same mean and variance) 
- The mean of the distribution of residuals is zero
















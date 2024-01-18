# Syllabus Class

I am not technically apart of this class yet (1/10/24)

# Artificial Intelligence (AI)

**********************************Intelligence displayed by Machines**********************************

## More practical definition of AI:

“Computational solutions to problems that traditionally require human intelligence”

- Strong/general artificial intelligence
    - Agents that are good at a large variety of tasks, can identify the task and then solve it
    - Simulation of Human intelligence
- Weak/narrow artificial intelligence
    - Intelligent agents focused on one task at a time

# Machine Learning (ML)

“Do not program an adult mind, but instead program a child’s mind and a way for it to learn.”

[[Test Data Set to test Algorithm]]

# Model Evaluation and Refinement
What is the [[Machine Learning Process]]?

From that process, you'll eventually cross the question of [[What is the goal of model development]]? There's quite the number of reasons of motivations for model development, but essentially each goal is different specifically, but overall it is to accomplish a set task or complete a given goal.

While in the process of all of this, you'll need to determine what [[Types of Machine Learning]] you'll use to train the model.

## Exercise...
A uh 'fun' [[Exercise to create a model]] that is quite... heavy. 

==I won't say that this is important, but it definitely is crazy==
#crazy #featureengineering #exercise

# Nearest Neighbors
[[Nearest Neighbor]]
- A very simple machine learning algorithm
- Given a labeled dataset, determine the label of a new point

- **Classify** a point as its nearest neighbor
	- Requires a definition of a distance

## The Equation (Euclidean Distance)
$$\sqrt{\sum_{i=1}^d (a_i - b_i)^2}$$
Essentially just the $c^2$ of $a^2 + b^2 = c^2$

## Euclidean ($L_2$) Distance
$$d(a,b) = \sqrt{\sum_{i=1}^d(a_i-b_i)^2}$$
Where: a,b are two vectors with dimensionality d
Sensitive to scale and therefore requires normalization (standardization)

You could do feature categories and overlap them to account for this potentially

# k-Nearest Neighbor
[[k-Nearest Neighbor]]

- Given a labeled dataset, determine the label of a new point
- 
## Strengths
- Simple and easy to implement
- Few assumptions made about the data
- Easily adapted for multi-class problems
- Computational effort for training is low
- Can be adapted for regression
## Weaknesses
- **Slow** (especially for large datasets)


# Nearest Centroid Classifier
- Training Phase
	- Calculate the centroid (mean vector) of each class
- Prediction Phase:
	- Given sample, $X_{new}$ assign label $Y_{new}$
	- Such that $Y_{new}$ is the closest class centroid

- Benefits and Drawbacks
	- Faster, especially for large datasets because it only compares to the number of classes, rather than number of datapoints
	- Doesn't model complex distributions - assumes a centroid describe the data well

# Gaussian/Normal Distributions
- Gaussian distributions are extremely common in the real world
- Gaussian distributions are a cornerstone of statistics, and many statistical equations *assume* data is normally distributed
- Machine learning often uses statistical models, so in machine learning we often *assume* the data is normally distributed.

## Estimating $\mu$ and $\sigma ^2$ 
A gaussian distribution is described by its mean ($\mu$) and variance ($\sigma ^2$)
$$\mu = \frac{1}{N}\sum_{i=1}^N x_i$$
Variance approximates the mean of difference between samples and mean
$$\sigma ^2 = \frac{1}{N-1} \sum_{i=1}^N (x_i - \mu)^2$$
Where N = the number of samples, and $x_i$ is a sample
==Note: Variance ($\sigma ^2$) is the standard deviation ($\sigma$) squared.==

# Modeling normally distributed data
$\mu$ and $\sigma^2$ are **sufficient statistics** - meaning we can recreate the entire distribution with just those two values
![[Pasted image 20240117142151.png]]

# Multivariate Gaussian Distribution
Details beyond the class on [[Multivariate Gaussian Distribution]].
**Multivariate gaussian distribution** is a gaussian distribution with more than 1 dimension

To describe it, we need:
- $\mu$ = a vector with the mean of each dimension
- $\Sigma$ = the covariance matrix, describing the variance among all dimensions
![[Pasted image 20240117142337.png]]

## Multivariate Mean ($\mu$)
More on [[Multivariate Mean]].
- This is the mean for each dimension
- We calculate mean independently for each dimension
![[Pasted image 20240117142427.png]]

### Avoiding common mistakes
- Make sure you correctly compute the mean!
- You should get a mean vector that has the same dimensionality as the number of features.
- The mean should NOT be a scalar value!
![[Pasted image 20240117142534.png]]

## Covariance
More on [[Covariance (Matrices)]].
- Given 2-dimensional data, we want to know
	- How much does X vary in dimension 1?
	- How much does X vary in dimension 2?
	- How much does dimension 1 vary relative to dimension 2
## $\Sigma$ 
$$cov(X^{(i)}, X^{(j)}) = \frac{\sum_{k=1}^{(i)}}{N-1}$$

## Covariance Matrix
- Describes the covariance between all dimensions of a dataset
- d x d mateix
	- where d = the number of dimensions
- Symmetric matrix
	- $cov(X^{(i)}, X^{(j)}) = cov(X^{(j)}, X^{(i)})$


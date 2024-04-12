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

# [[Decision Trees]]
- Decision trees are designed to work with non-numeric data
	- Binary features (Yes/No, True/False)
	- Categorical features
- Their goal is to best divide the data (to make a decision)
- Data is split one feature at a time which forms a tree-structure with data splits at each node
- How the data is split can be posed as a question which means decision trees are highly interpretable

## An Example Dataset
Consider the following dataset containing 8 samples and 2 features

| Features | Class |
| ---- | ---- |
| $x_1$ = <t,d> | $y_1$ = + |
| $x_2$ = <s,d> | $y_2$ = + |
| $x_3$ = <t, b> | $y_3$ = - |
| $x_4$ = <t,r> | $y_4$ = - |
| $x_5$ = <s,b> | $y_5$ = + |

Height = (Tall, Short)
Hair = (Dark, Blonde, Red)

## Decision Stump
- The complexity of the classification function depends on the depth of the decision tree
- A depth-1 decision tree is called a **decision stump**

## Decision Tree
- The deeper the tree, the more complex the classification function
- There is no limit to the depth of the decision tree

## Decision Tree Algorithm
High level view of a decision tree for a binary classification task:
**Algorithm: divide(*data*)** 
1. If (all classes are the same in data)
2. return
3. *feature* = find_feature_which_best_splits( data )
4. data_yes, data_no = split_by( feature, data )
5. divide( data_yes )
6. divide( data_no )

## Splitting the Data
- Random Baseline = randomly choose which feature to split
- Based on Class Ratio?:
	- For each number, count the number of samples in the true class and the number of samples in the false class
	- Select the feature which has the best class ratio (i.e. most true samples in the split)?
	- No guarantee it will be a good split in the long run
	- What about the other node (which split to consider?)
Information Theory to the rescue!

## [[Information Theory]]
- What is information?
	- Information reduces uncertainity
	- Information is relative to what you already know
	- The information content of a message is related to how surprising the information is.
	- Therefore, information relies on the information that you already know, so therefore information relies on context.

![[Pasted image 20240119142421.png]]
## What is a "Surprising Message"
- Surprise is something you don't expect ( #interesting )
- Suppose I have a coin with heads on both sides
	- I flip the coin and tell you the outcome was heads
	- How much information did you gain?
- Suppose I have a normal (fair) coin?
	- I flip the coin and tell you the outcome was heads
	- How much information did you gain?

# Information as Bits
- Assume messages are conveyed with bits (0 or 1)
- Conveying the outcome of a fair coin toss requires 1 bit of information
	- It conveys one of two equally likely outcomes
- Conveying an outcome that is certain requires 0 bits
- Conveying the outcome of an experiment with 8 equally likely outcomes requires 3 bits
	- $2^3 = 8$ <- encode each outcome to a bit string
		- 0 0 0 
		- 0 0 1
		- 0 1 0
		- 0 1 1
		- 1 0 0 
		- 1 0 1
		- 1 1 1

# Information as Probability
- In general, if an outcome has a probability $p$, the information content of the message describe that outcome is: $$I(p) = -log_2(p)\ \ \& \ \ I(0) = 0$$
That is, information content of message conveying an outcome is the negative log of the probability of that outcome occurring

For example: Conveying the outcome of an experiment with 8 equally likely outcomes requires 3 bits
That is, each outcome has probability 1/8:$$I(0.125) = -log_2(0.125) = -(3) = 3$$
And therefore each message about the outcome of the experiment has an information content of 3 bits

## Information is Subjective
![[Pasted image 20240119143233.png]]

## Information and [[Shannon's Entropy]]
- Suppose we have a message that conveys the result of a random experiment with *m* possible discrete outcomes
- Each outcome has the probability: $p_1, p_2, p_3, ..., p_m$
- The expected information content of that message is called the entropy of the probability distribution:$$Entropy = H(p_1, p_2, ..., p_m) = \sum_{i=1}^m p_i * I(p_i)$$
- $$Information = I(p) = -log_2(p)\ \ \& \ \ I(0) = 0$$

## [[Shannon's Entropy]] as a Measure of Information
Let $\vec{P}$ be a discrete probability distribution:$$\vec{P} = <p_1, P_2, ... p_m>$$
The entropy of the distribution, $\vec{P}$ is given by: $$Entropy = H(\vec{P}) = \sum_{i=1}^m p_i * I(p_i) = - \sum_{i=1}^m p_i * log_2(p_i)$$
## [[Shannon's Entropy]]
- Shannon's Entropy gets more interesting when the probabilities of each outcome are not the same $$\vec{P} = <0.7, 0.2, 0.1>$$
![[Pasted image 20240119144018.png]]

# [[Estimating Generalization]]
- Remember: generalization is the goal
	- maximize the model's performance on novel (unseen) data
	- That is, maximize the model's performance on test/validation data
- Training accuracy is often optimistic with the respect to the novel data
- We estimate generalization using:
	- Hold out or, even better [[Cross-Validation]]

## Simple Test/ Train Split
![[Pasted image 20240124191238.png]]

## Example of Overfitting with a Decision Tree
![[Pasted image 20240124191312.png]]

# [[Overfitting]]
- Overfitting relates to training error decreasing at the expense of model generalization
<mark style="background: #ADCCFFA6;">Minimizing training error does not necessarily minimize generalizability (test/validation)</mark> 
![[Pasted image 20240124191630.png]]

## What causes Overfitting?
- How does it happen?
	- Poor sampling/ Outliers
	- Overtraining
	- Poor algorithm selection / hyperparameter selection, etc...
- **[[Hyperparameter]]** = an input parameter to a machine learning algorithm that controls the learning process and is not learned during training.

# [[Overtraining]]
- Overtraining
	- Training a model for too many epochs
	- Making improvements to training error at the expense of validation error
- [[Epochs|Epoch]] = 1 iteration over the training data
- How to avoid overtraining?
	- Monitor test/ validation error loss
	- Introduce heuristics such as max-depth for a decision tree
	- Introduce regularization, drop out, etc... (these will be discussed later in the course)
![[Pasted image 20240124192143.png]]

# Poor Algorithm / Hyperparameter Selection
- Choosing good hyperparameter values (e.g. max depth) can help prevent overfitting
- Choosing an appropriate algorithm can help prevent overfitting
	- E.g. use a linear classifier for linear data

# Use [[Cross-Validation]] to Tune [[Hyperparameter]]s
- Help prevent the effect of bad sampling / outliers
- Helps to choose hyperparameter values that generalize well
- **[[Grid-Search]]**:
	- A common way to tune (optimize) hyperparameters
	- Try a bunch of values in an ordered (grid-like) manner
- Try a bunch of values and choose the one that performs best on the validation/test data

# [[Hold Out Method]]
![[Pasted image 20240124193043.png]]

![[Pasted image 20240124193219.png]]

![[Pasted image 20240124193238.png]]

# [[K-Fold Cross-Validation]] (K=5)

![[Pasted image 20240124193313.png]]

![[Pasted image 20240124193515.png]]

- Calculate performance metric for each fold
- Report the metric averaged over all folds
$$P=\frac{1}{k} \sum_{i=1}^{k} p_i$$
Where $P$ is overall performance, $p_i$ is the performance metric for fold $i$ and $k$ is the number of folds

## Theory Behind This
### [[Bias-Variance Trade-Off]]
- Variance - the amount that your model is sensitive to the data
	- If variance is higher, then performance will differ a lot between runs of Cross-Validation
- Bias - the amount of assumptions (bias) built into the model
	- If bias is high, then performance will differ little between runs of Cross-Validation
- "**bias** is reduced by using only local information"
- "**variance** can only be reduced by averaging over multiple observations, which inherently means using information from a larger region."
<mark style="background: #ADCCFFA6;">Question: In KNN, how does increasing K affect bias/variance?</mark>

| Complex Models | Simple Models |  |
| ---- | ---- | ---- |
| High Variance | Low Variance |  |
| Low Bias | High Bias<br> |  |
Complex models (e.g. high degree polynomials) are highly dependent on the training data (high variance): Prone to [[Overfitting]]

Simple models (e.g. linear models) have strong assumptions which prevents them from fitting the data too closely. However: Prone to [[Underfitting]]

## Decision Tree Depth and Bias / Variance
![[Pasted image 20240124194149.png]]

# [[Underfitting]] and [[Overfitting]]
![[Pasted image 20240124194605.png]]

# [[Outliers]] and [[Bias]]
- Simple models reduces the effects of outliers
	- We want to reduce the influence of outliers
	- We want the model to fit a more global mean
![[Pasted image 20240126141334.png]]

# Notes On Cross-Validation
![[Pasted image 20240126142032.png]]

## Good Practices
Shuffle your data before doing a test/train split
- Ordering may be present in the data
	- On purpose or inadvertently
- You don't want the ordering to bias the test/train split or k-fold split
	- And therefore create data with different distributions
<mark style="background: #BBFABBA6;">Tip: Shuffling your data, then sequentially splitting makes dividing it into buckets easier anyway</mark>
![[Pasted image 20240126142242.png]]

![[Pasted image 20240126142306.png]]

### Stratified Split
- You should ensure a similar class distribution for splits as is present in the whole dataset
### Train using the data's true class balance
- When workin with imbalanced datasets it is best to try to train with the natural class ratio
	- This should be your default option

![[Pasted image 20240126142443.png]]


---

# The [[Perceptron]]
- An early linear classifier
- Iteratively updates the weights to find a line that divides the data perfectly
	- Sign of output is used as class
- Performs binary classification
	- Encodes positive class as +1, and negative class as -1

![[Pasted image 20240126144646.png]]

- Assumes data is linearly separable
- No guarantee of convergence for non linearly separable data
- No guarantee of optimality
	- Furthermore, no guarantee it gets better over time

# [[Regression]]
- In regression, we are estimating the relationship between inputs and outputs
"As temperature increases, fan speed increases"
"As outside temperature and sunniness increase, cooling energy requirements increase"

- Statistically
	- Estimating the relationship between independent and dependent variables
	- Independent var is input
	- Dependent var is output
- Graphically
	- Curve-fitting, surface fitting, function approximation

# [[Linear Regression]]
- Most real-world relationships are NOT linear, however:
	- Many processes can be approximated
	- LR can be solved by hands
	- LR is good intro to machine learning
	- LR is used as part of larger machine learning models

- Because we assume there is a linear relationship between inputs and outputs
- We create our model that defines this linear relationship
- At it's most basic, this is the slope of the line and the y-intercept
	- Y-intersect is called the bias and defines the height of the line

- For multiple dimensions the line is defined by its slope for each dimension
- Still a single bias
- It creates a plane or hyperplane defined as: $$\hat{y} = b + \theta^{(1)}x^{(1)} + \theta^{(2)}x^{(2)} + ... + \theta^{(d)}x^{(d)}$$
- We call the set of parameters defining the [[Hyperplane]] the weights (indicated by theta ($\theta$))

## Vector Notation
Given a hyperplane of a d dimensions: $$\hat{y} = b + \theta^{(1)}x^{(1)} + \theta^{(2)}x^{(2)} + ... + \theta^{(d)}x^{(d)}$$
We can use a compact vector representation by adding a bias dimension each sample 
($x^{(0)} = 1$)
$$\hat{y} = b + \theta^{(0)}x^{(0)} + \theta^{(1)}x^{(1)} + \theta^{(2)}x^{(2)} + ... + \theta^{(d)}x^{(d)}$$
$$\hat{y} = \theta x$$
## Generalized problem set up
![[Pasted image 20240129142225.png]]

## [[Mean Squared Error]]
$$J(\theta) = \frac{1}{n}\sum_{i=1}^{n}(y_i - \hat{y}_i)^2$$
$$= \frac{1}{n}(Y-X\theta)^T(Y-X\theta)$$


## Training - Problem Set Up
![[Pasted image 20240129143222.png]]

## Geometric Interpretation
$$J(\theta) = \frac{1}{n}\sum_{i=1}^{n}(y_i - \hat{y}_i)^2 = J(\theta) = \frac{1}{n}\sum_{i=1}^{n}(y_i - x_i\theta)^2$$
- Our dataset is fixed, so we treat Y and X as fixed
	- Therefore: Sum of Squared Errors is a quadratic equation
	- A quadratic is a polynomial with highest order of 2
	- When plotted quadratics from paraboloids
	- Paraboloid = quadric surface

![[Pasted image 20240129143508.png]]

• Our goal is to minimize loss 
• The paraboloid is a surface defined by the loss 
• Minimum loss is the low point on the surface

• Our loss is a paraboloid and is therefore differentiable, and it has a single location where the derivative is 0
• We can find the minimum by following the slope until we arrive at the minimum

"Learning is about finding the low point on the objective function"

## How to solve
- Two methods
	- Least Squares Estimation
		- Closed Form Solution
		- Analytical (all at once) - more efficient if possible
	- Gradient Descent
		- Iterative - more flexible solution method

## [[Least Squares Estimation]]

$$\frac{1}{n}(Y^TY-Y^TX\theta - X^T\theta^TY + X^T\theta^TX\theta)$$

## [[Gradient Descent]]
![[Pasted image 20240131141343.png]]

- The iterative solution is most commonly used in practice
- Avoids/reduces memory and computational requirements
- Works with more loss functions
- Guarantee the optimum solution in theory, but not in practice
- Requires [[hyperparameter]] tuning

1. Start somewhere on the loss surface
2. Find the direction to move
3. Move in that direction
4. Repeat steps 2 and 3

### [[Learning Rate]]
- The learning rate is used in the update step (step 2) of gradient descent
- It scales the step size =amount we move (adjust $\theta$)
$$\theta_{new} = \theta - \eta \frac{1}{n}X^T(\hat{Y} - Y)$$
- Too high and you bounce around the solution
- Too low and you won't reach the solution before stopping
- Typically it is a scalar, but it could be a vector (1xd)
- Can be fixed, or decrease with time

### [[Stopping Conditions]]
- Gradient descent can take a long time to converge
- If we make the learning rate too high, it may never converge (and therefore never stop)
- We add stopping conditions
	- Maximum number of [[epochs]] and/or small enough loss

- Stop when number of epochs > max_epoch
- Stop when loss is < min_loss

## Linear Regression
```pseudo
1. Initialize theta (vector of 0's)
2. While stopping conditions are not met
	1. learning rate equation
3. Output model parameters(theta)
```

## Least Squares Estimation (Analytical)
$$\theta = (X^TX)^{-1}X^TY$$

# [[Polynomial Regression]]
- What about when our data is not linearly related?
	- We can perform polynomial regression
- The degree of a polynomial indicates the number of degrees of freedom it has
	- The number of inflection points
	- Its ability to bend

- If we don't know how the data is related, we have to guess what degree of polynomial to fit
	- This is typical

- Prone to overfitting the data
- Numerically unstable
	- Huge fluctuations from small weight changes
- Non-loca relationship fluctuations

## High Degree Polynomials
- Non-local fluctuations mean that its unpredictable beyond observed
- The higher the degree, the more the problem

## Choosing the Degree
- Use a grid search and cross-validation
- Choose the polynomial degree that has the best average validation performance
- Cross-validation should help your detect overfitting and numerical instability

## [[Hypersurfaces]]
- Linear regression is linear per dimension and forms a hyper-plane

- Polynomial regression is polynomial per dimension
	- e.g. for a polynomial of degree 3 and a sample with 3 features (and a bias)

## Polynomial Regression Math
Consider regressoin using the mean squared error as a loss function

## [[Z-Scaling]]
It is sometimes best to standarize data using covariance
- Since learning rate is shared across all dimensions it makes the learning rate relative to feature scaling consistent across dimensions
- It can help with numerical instability issues for polynomial regression
Z-Scaling:
- Convert a value ($x$) to standard scaled value ($z$)
	- Subtract out the mean ($\mu$) and divide by the standard deviation ($\sigma$)

## Question
- We have data with 4 features
- We apply a polynomial basis function of degree 10 and add a bias
<mark style="background: #FFB86CA6;">What is the dimensionality of our new X matrix?</mark> <mark style="background: #BBFABBA6;">41</mark> (10 degrees per feature + 1 bias)
<mark style="background: #FFB86CA6;">How many inflection points can our curve have?</mark> <mark style="background: #BBFABBA6;">9</mark> 

# Small Review
## [[Overfitting]]
- Saw it was easy to overfit data with polynomial regression
- Reduces generalizability of model
- Overfitting relates to training error decreasing at the expense of model generalization
## [[Overtraining|Generalization]] and [[Overfitting]]
- Generalization is the goal
	- Maximize mdoel's performance on novel data
- Training error reports performance with respect to seen data
- Training error is often optimistic with respect to novel data

## How to prevent overfitting
- Use cross validation to tune hyperparamters
- Regularization
- Other methods
	- Early stopping
	- Dropout
## [[Underfitting]]
- Too simple of a fit to a model
- Model has too much bias and is therefore not sensitive enough to the data

# [[Regularization]]

- We redefine the loss function to account for both training error (how well we fit the sampled data) and model complexity
$$Loss = Error + \lambda * Complexity$$
$\lambda$ is a hyperparameter that weights the trade-off between training error and complexity

# [[L2 Regularization]]
$$J(\theta) = Error + \lambda \theta^T \theta$$
• L2 Regularization estimates complexity as the squared sum of weight values 
• This is the squared L2 Norm of the weight vector
- Recall the $L_2$ norm is: $$L_2Norm = \sqrt{\sum_{i=1}^d(\theta_i)^2}$$

- $L_2$ Norm is also known as the Euclidean norm
- With $L_2$ regularization the $L_2$ Norm is squared for computational simplicity

# [[Ridge Regression]]
- Ridge Regression is regression that uses mean squared $L_2$ error and $L_2$ regularization. Therefore, the loss function is:$$J(\theta) = \frac{1}{n}(Y-X\theta)^T(Y-X\theta)+\lambda \theta^T\theta$$

---
Missed a few slides
---
#todo 

---

# [[Maximum Likelihood Estimate]]

## Maximum Likelihood Estimate Matrix Form

## Calculating the Maximum Likelihood Estimate 

## Calculating the Maximum Likelihood Estimate with Linear Function

## MLE is Flexible
$$L(Y|X, \theta) = \prod_{i=1}^n p(y_i|x_i, \theta)$$

## Bernoulli Distribution
## [[Logistic Regression with MLE]]

# Binary Cross Entropy

## Normalized Binary Cross Entropy

## Matrix Form

# [[Neurons]]

# [[Back Propagation]]

# Different Activation Functions
- You can use different activation functions for hidden layers with minimal changes to the back propagation algorithm
	- Activation Functions should be differentiable for the chain rule to work
	- Activation Functions should have derivatives that are easy to calculate for efficiency


## [[Vanishing Gradient]] Problem

## Tanh function
$$f(x) = tanh(x) = \frac{2}{1+e^{-2x}}-1$$
- tanh function is often used instead of logistic
- Unlike logistic, its range is -1 to 1. This is a greater range meaning that it is often steeper
	- This it has a higher gradient which can reduce the vanishing gradient problem

## [[ReLu]] Function
- Just like tanh and logistic, ReLu is nonlinear, so it can be used nonlinear regression problems
- Not truly differentiable, but differentiable in practice
	- If input <= 0, derivative is 0, else derivative is 1
- Benefits:


# Optimization Algorithms
- Optimization algorithms define how you update at each step
- All optimization algorithms work "like gradient descent"
	- You are searching a space defined by weights and loss
	- You move in the direction of the derivative
- Each algorithm
	- Different claims on how they overcome challenges in the optimization function

## Common Optimization Algorithms
These algorithms use batch-based updates
The differences between them are technical and aren't important
- Gradient Descent
- Gradient Descent with Momentum
- RMS Prop
- AdaGrad
- Adam (ADaptive MOment optimizer)

# Data Balance
**Breast Cancer Dataset**
- 458 benign and 241 malignant
- Fairly balanced, ~2 to 1 class balance
**Iris Dataset**
- 50 of each flower (3 flowers)
- Perfect 1 to 1 to 1 balance


| Relationship | Definition | Example |
| ------------ | ---------- | ------- |
| TrIP         |            |         |
| TrWP         |            |         |
| TrCP         |            |         |
| TrAP         |            |         |
| TrNAP        |            |         |
| TeRP         |            |         |
| TeCP         |            |         |
| PIP          |            |         |

# Machine Learning Process
- Training is only a small part of machine learning
- Data collection, feature engineering, developing a model, and model refinement take most of your time

Mainly collecting, cleaning, and organizing data takes a lot of time

## Dealing with Data
- Data Collection
	- Identify data sources, collect, and extract the data into some useable format
- Data Cleaning
	- Imputing missing values, removing outliers, normalizing data, removing invalid samples, etc..
- Feature Engineering (feature extraction)
	- Creating informative features from the cleaned data
- Feature Selection
	- Selecting (or removing) features that are helpful for your end-goal

### Breast Cancer Dataset
Collect and digitize images of a fine needle aspirate (FNA) of a breast mass
Ensure all images are valid (no problems with imaging or digitization)

1. Identify cell nuclei boundaries
2. Characterize nuclei in terms of: radius, perimeter, area, compactness, smoothness, concavity, concave points, symmetry, dimension, and texture

Scale feature values between 1 and 10

From the 10 features, select a set of 4 informative features by trying different combinations and seeing which gives best test set performance

## Data Collection

## Data Cleaning

## Data Cleaning: Imputation




# Weak Learning
Are many simple learners better than a single complex learner?

They can be, because it can prevent overfitting

Ensemble methods are ways to combine the results of many learners, typically weak learners
1. Stacking
2. Bagging
3. Boosting

• Weak Learner – a classification or regression algorithm that performs poorly. Usually (but not strictly) they are computationally simply. Weak learners typically are less prone to overfitting 
• Ensemble Method – a method to combine the outputs of different algorithms. Ensemble methods hope to lessen the potential for overfitting 
• Stacking – an ensemble method that uses the outputs of classifiers as input into another classifier 
• Bagging – an ensemble method that uses bootstrap sampling to generate many models on a dataset
• Boosting – an ensemble method in which classifiers are applied sequentially, and the prediction performance of one classifier affects how the next classifier is built

# Ensemble Methods
## Stacking
- Several model outputs are input into another model
- Ensemble methods can be used with any learner
	- It doesn't have to be a weak learner


# Project 3 Ideas
- Spending variance per customer
	- Customer typically spends between $100-$500, if they spend $10,000 something is wrong
- Time of day (morning, afternoon, evening, night)
- Time between transactions
- Transactions on the weekend (didn't really add performance)
- CVV Match
	- Input vs. Actual CVV (Didn't do much apparently?)
- F1 Score as a function of Threshold
	- Messing with threshold?
- SMOTE/Undersampling
	- Split data into buckets, then undersample the bucket
- PCA
	- I don't really get this
- XGBoost

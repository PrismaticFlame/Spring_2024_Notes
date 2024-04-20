

# Midterm 1 Review

## [Exam 1](../Spring_24/midterm_review.pdf)
- Math background
	- Normal distributions, variance, covariance
	- Basic matrix operations
- Machine learning process
- Hyper parameter tuning
- Feature engineering
- Data normalization
- Overfitting and underfitting
	- Bias and Variance
	- Cross-validation
	- Regularization
		- L1 and L2
	- Loss Functions
		- Mean Squared Error
		- Binary Cross Entropy
	- Gradient Descent
		- "vanilla", stochastic, mini-batch
- KNN Classifier
	- Distance measures
- Nearest Centroid Classifier
- Decision Trees
	- Information Theory
- Perceptron
- Linear Regression
- Polynomial Regression
- Logistic Regression
- Artificial Neural Networks
	- Structure
	- Back Propagation

### Covariance
$$
\begin{matrix}
var(x_1) & cov(x_n, x_1) \\
cov(x_n, x_z) & var(x_n) \\
\end{matrix}
$$

- Diagonal elements: the variance of a single dimension
- Off diagonal elements: The covariance between those two features
- Always symmetric
- Feature 1 and 2 have high covariance means when 1 goes up, so does 2
- Feature 1 and 2 have high negative covariance means when 1 goes up, 2 goes down
### Overfitting, Underfitting, and Cross Validation
- Test set vs. Validation set
	- Test is held out during model development, it is used to evaluate the system after all hyper-parameters have been tuned. Validation set is held out during model training, but used to evaluate during hyper-parameter tuning and model selection
- Bias and variance trade-off relates to model complexity:
	- Simpler model = more bias, less variance
	- Complex models = less bias, more variance
- How to decrease potential overfitting in K-Nearest Neighbors algorithm?
	- Increase k
- How to decrease potential overfitting in polynomial regression
	- Choose smaller degree
	- Add regularization

### Linear, Polynomial, and Logistic Regression
- How does an objective function relate to the weights of our model?
	- The objective function determines the loss for a particular choice of weights
	- We can plot it, and it is a plot of model weights versus the loss of the corresponding model
- Why do we want where the gradient is zero?
	- That is the minimum value of our objective function(loss function), which tells us where the best model weights are
- Analytical solution for an objective function that is convex? Intuition behind the solution?
	- Take the derivative, set the equation to 0, and solve for theta. This is equivalent to finding the values of theta that minimize the objective
	- A convex function has a single global minimum which is where the derivative is zero.
- Why want objective function to be convex?
	- For a global minimum
- Binary Cross Entropy and when is it used?
	- It's a loss function, and is used primarily for binary classification
- Mean Squared Error and when is it used?
	- It's a loss function, and is primarily used for regression

### Gradient Descent
- What is an epoch?
	- An iteration over the entire dataset
- What are you descending in gradient descent?
	- The loss function (to find the minimum)
- 

## Hyperparameters
- KNN Classifier
	- K, Distance Measures
- Nearest Centroid Classifier
	- Distance measures
- Decision Trees
	- Splitting Criteria, Max Depth
- Perceptron
- Linear, Polynomial, Logistic Regression
	- Maybe: learning rate, momentum
	- Regularization method
	- Function: linear, logistic, polynomial degree
	- Loss Function: Binary Cross Entropy, Sum of Mean Squared Error (or Mean Squared Error)
- Artificial Neural Networks
	- Number of hidden neurons
	- Early stopping and/or regularization method




# After Midterm 1





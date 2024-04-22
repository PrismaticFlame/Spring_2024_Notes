Gradient Descent is an optimization algorithm used to minimize the cost or loss function in machine learning models, especially in the context of training neural networks and other iterative optimization problems. The goal is to find the minimum of a function by iteratively moving in the direction of the steepest decrease in the function.

### Key Concepts:

1. **Objective Function:**
   - In machine learning, the objective function is typically a cost or loss function that measures the difference between the predicted values of the model and the actual values.

2. **Optimization:**
   - The goal of Gradient Descent is to find the set of parameters that minimizes the objective function. These parameters are often the weights in a machine learning model.

3. **Gradient:**
   - The gradient is a vector that points in the direction of the steepest increase in the function. The negative gradient points in the direction of the steepest decrease.

### Basic Idea:

1. **Initialization:**
   - Start with an initial guess for the parameters.

2. **Iterative Update:**
   - Iteratively update the parameters in the direction of the negative gradient of the objective function.

3. **Convergence:**
   - Repeat the process until convergence is achieved. Convergence is typically determined by reaching a certain number of iterations or when the change in the objective function becomes small.

### Mathematically:

Given a cost function \(J(\theta)\) where \(\theta\) represents the parameters (weights) of the model, the update rule in each iteration of Gradient Descent is given by:

$$\theta = \theta - \alpha \nabla J(\theta)$$

Here:
- $\alpha$ is the [[Learning Rate]], a hyperparameter that determines the size of the steps taken in each iteration.
- $\nabla J(\theta)$ is the gradient of the cost function with respect to the parameters \(\theta\).

### Types of Gradient Descent:

1. **Batch Gradient Descent:**
   - Uses the entire dataset to compute the gradient of the cost function in each iteration. Computationally expensive for large datasets.

2. **[[Stochastic Gradient Descent (SGD)]]:**
   - Uses only one randomly chosen data point to compute the gradient in each iteration. Faster but can have more noisy updates.

3. **[[Mini-Batch Gradient Descent]]:**
   - Uses a small random subset (mini-batch) of the dataset to compute the gradient. Balances the trade-off between computational efficiency and noise in updates.

### Learning Rate:

- The learning rate (\(\alpha\)) is a crucial hyperparameter. If it is too small, the algorithm may converge very slowly. If it is too large, the algorithm may overshoot the minimum and fail to converge.

### Convergence Criteria:

- Convergence is typically checked based on the change in the value of the cost function or when the gradient becomes very small.

### Example (Python - Batch Gradient Descent):

```python
import numpy as np

def gradient_descent(X, y, theta, learning_rate, num_iterations):
    m = len(y)
    
    for _ in range(num_iterations):
        predictions = X.dot(theta)
        errors = predictions - y
        gradient = 2/m * X.T.dot(errors)
        theta = theta - learning_rate * gradient
    
    return theta

# Example usage
X = np.array([[1, 2], [1, 3], [1, 4]])  # Features with added bias term
y = np.array([2, 5, 9])  # Target variable
theta = np.zeros(X.shape[1])  # Initial guess for parameters

# Set hyperparameters
learning_rate = 0.01
num_iterations = 1000

# Run gradient descent
theta = gradient_descent(X, y, theta, learning_rate, num_iterations)

print("Final Parameters:", theta)
```

In this example, Batch Gradient Descent is used to find the parameters (\(\theta\)) that minimize the cost function. The algorithm iteratively updates the parameters until convergence. Note that in practice, more advanced variations of gradient descent (like mini-batch or stochastic gradient descent) are often used for large datasets or complex models.
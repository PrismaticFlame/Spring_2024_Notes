Stochastic Gradient Descent (SGD) is an optimization algorithm used for training machine learning models, particularly in the context of large-scale datasets. It is a variant of the traditional gradient descent algorithm that updates the model parameters based on a single randomly chosen data point (or a small subset) in each iteration. This randomness in selecting data points makes SGD computationally efficient and suitable for online learning scenarios.

### Key Characteristics of Stochastic Gradient Descent:

1. **Random Sampling:**
   - In each iteration, a single data point (or a small random subset, known as a mini-batch) is selected to compute the gradient and update the model parameters.

2. **Efficiency:**
   - SGD is computationally more efficient than batch gradient descent, especially for large datasets, as it processes only a fraction of the data in each iteration.

3. **Noisy Updates:**
   - Due to the random selection of data points, SGD updates can be noisy. This noise can help the algorithm escape local minima and explore the parameter space more effectively.

4. **Online Learning:**
   - SGD is well-suited for online learning scenarios where the model is updated continuously as new data becomes available.

5. **[[Learning Rate]]:**
   - The learning rate in SGD can be more critical than in batch gradient descent. Common strategies include using a fixed learning rate, learning rate schedules, or adaptive learning rate methods.

### SGD Update Rule:

The update rule in SGD is similar to that of batch gradient descent but involves the contribution of a single data point:

$\theta = \theta - \alpha \nabla J_i(\theta)$

Here:
- $\alpha$ is the learning rate.
- $\nabla J_i(\theta)$ is the gradient of the cost function with respect to the parameters \(\theta\) based on the chosen data point.

### Python Example:

```python
import numpy as np

def stochastic_gradient_descent(X, y, theta, learning_rate, num_epochs):
    m = len(y)
    
    for epoch in range(num_epochs):
        for i in range(m):
            rand_index = np.random.randint(m)  # Randomly choose a data point
            X_i = X[rand_index:rand_index+1]
            y_i = y[rand_index:rand_index+1]
            
            predictions = X_i.dot(theta)
            errors = predictions - y_i
            gradient = 2 * X_i.T.dot(errors)
            theta = theta - learning_rate * gradient
    
    return theta

# Example usage
X = np.array([[1, 2], [1, 3], [1, 4]])  # Features with added bias term
y = np.array([2, 5, 9])  # Target variable
theta = np.zeros(X.shape[1])  # Initial guess for parameters

# Set hyperparameters
learning_rate = 0.01
num_epochs = 100

# Run stochastic gradient descent
theta = stochastic_gradient_descent(X, y, theta, learning_rate, num_epochs)

print("Final Parameters:", theta)
```

In this example, the `stochastic_gradient_descent` function implements SGD for a simple linear regression model. It updates the parameters based on a single randomly chosen data point in each iteration. Note that in practice, mini-batch SGD is often preferred, where a small random subset of data points is used for each iteration to balance the noise and computational efficiency.
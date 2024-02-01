Mini-Batch Gradient Descent is a compromise between Batch Gradient Descent and Stochastic Gradient Descent. In this optimization algorithm, the model parameters are updated based on a small random subset of the training data in each iteration. This subset is called a "mini-batch." Mini-Batch Gradient Descent combines the efficiency of stochastic gradient descent with the stability of batch gradient descent and is commonly used in practice for training machine learning models.

### Key Characteristics of Mini-Batch Gradient Descent:

1. **Random Sampling:**
   - In each iteration, a random mini-batch of data points (typically ranging from tens to a few hundred) is selected to compute the gradient and update the model parameters.

2. **Efficiency:**
   - Mini-Batch GD is computationally more efficient than Batch GD, as it processes only a subset of the data in each iteration, making it suitable for large datasets.

3. **Reduced Variance:**
   - Compared to Stochastic GD, mini-batch updates introduce less noise due to the averaging effect of the mini-batch, resulting in more stable convergence.

4. **Parallelization:**
   - Mini-Batch GD can take advantage of parallel processing since different mini-batches can be processed concurrently on multiple processors or GPUs.

5. **[[Learning Rate]] Adjustment:**
   - The learning rate becomes more critical in Mini-Batch GD. Common strategies include using a fixed learning rate, learning rate schedules, or adaptive learning rate methods.

### Mini-Batch Update Rule:

The update rule in Mini-Batch GD is a variation of the gradient descent update rule:

$\theta = \theta - \alpha \nabla J_{\text{mini-batch}}(\theta)$

Here:
- $\alpha$ is the [[learning rate]].
- $\nabla J_{\text{mini-batch}}(\theta)$ is the gradient of the cost function with respect to the parameters $\theta$ based on the selected mini-batch.

### Advantages of Mini-Batch Gradient Descent:

1. **Computational Efficiency:**
   - It is computationally more efficient than Batch GD, making it suitable for large datasets.

2. **Stability:**
   - It provides more stable convergence compared to Stochastic GD due to the averaging effect of the mini-batch.

3. **[[Parallelization]]:**
   - Mini-batch processing allows for parallelization, making it possible to take advantage of multi-core CPUs or GPUs.

### Python Example:

```python
import numpy as np

def mini_batch_gradient_descent(X, y, theta, learning_rate, num_epochs, batch_size):
    m = len(y)
    
    for epoch in range(num_epochs):
        shuffled_indices = np.random.permutation(m)
        X_shuffled = X[shuffled_indices]
        y_shuffled = y[shuffled_indices]
        
        for i in range(0, m, batch_size):
            X_mini_batch = X_shuffled[i:i+batch_size]
            y_mini_batch = y_shuffled[i:i+batch_size]
            
            predictions = X_mini_batch.dot(theta)
            errors = predictions - y_mini_batch
            gradient = 2/batch_size * X_mini_batch.T.dot(errors)
            theta = theta - learning_rate * gradient
    
    return theta

# Example usage
X = np.array([[1, 2], [1, 3], [1, 4]])  # Features with added bias term
y = np.array([2, 5, 9])  # Target variable
theta = np.zeros(X.shape[1])  # Initial guess for parameters

# Set hyperparameters
learning_rate = 0.01
num_epochs = 100
batch_size = 2  # Mini-batch size

# Run mini-batch gradient descent
theta = mini_batch_gradient_descent(X, y, theta, learning_rate, num_epochs, batch_size)

print("Final Parameters:", theta)
```

In this example, the `mini_batch_gradient_descent` function implements Mini-Batch Gradient Descent for a simple linear regression model. The parameters are updated based on randomly selected mini-batches in each iteration. The `batch_size` parameter determines the size of each mini-batch.
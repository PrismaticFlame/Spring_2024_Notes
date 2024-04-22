L2 regularization, also known as Ridge regularization or Tikhonov regularization, is a technique used in machine learning and statistics to prevent overfitting and stabilize the model by adding a penalty term based on the squared magnitudes of the model coefficients to the objective function being optimized.

### L2 Regularization Formula:

The L2 regularization term is added to the original loss function, and the new objective function becomes:

$J(\theta) = \text{Original Loss} + \lambda \sum_{i=1}^{n} \theta_i^2$

Here:
- \( J(\theta) \) is the new objective function with L2 regularization,
- \(\text{Original Loss}\) is the loss term from the original objective function,
- \(\lambda\) (lambda) is the regularization parameter that controls the strength of regularization,
- \(\sum_{i=1}^{n} \theta_i^2\) is the sum of the squared coefficients (excluding the intercept term).

### Key Points about L2 Regularization:

1. **Shrinkage Effect:**
   - L2 regularization penalizes large values of the coefficients, effectively shrinking them towards zero. This helps prevent overfitting by discouraging overly complex models.

2. **Trade-Off:**
   - The choice of the regularization parameter (\(\lambda\)) is crucial. A larger \(\lambda\) increases the regularization strength, resulting in more significant shrinkage of coefficients. However, setting \(\lambda\) too high may lead to underfitting.

3. **Equivalent to Weight Decay:**
   - In optimization algorithms, the L2 regularization term is equivalent to adding a penalty term to the weights during the weight update. This is sometimes referred to as weight decay.

4. **Global Shrinkage:**
   - L2 regularization applies a global shrinkage to all coefficients. It doesn't enforce sparsity (setting some coefficients exactly to zero), but it encourages small values for all coefficients.

5. **Robustness to Multicollinearity:**
   - L2 regularization can help improve the stability of models in the presence of multicollinearity, where predictor variables are highly correlated.

### Python Example:

Let's use the same linear regression example as before, but this time with L2 regularization (Ridge regression) using scikit-learn:

```python
from sklearn.linear_model import Ridge
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error
import numpy as np

# Generate synthetic data
np.random.seed(42)
X = 2 * np.random.rand(100, 1)
y = 4 + 3 * X + np.random.randn(100, 1)

# Split the data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Create Ridge regression model with regularization parameter (alpha)
ridge_model = Ridge(alpha=1.0)

# Fit the model to the training data
ridge_model.fit(X_train, y_train)

# Make predictions on the test data
y_pred = ridge_model.predict(X_test)

# Evaluate the model
mse = mean_squared_error(y_test, y_pred)
print("Mean Squared Error:", mse)
```

In this example, the `Ridge` regression model from scikit-learn is used with an `alpha` parameter controlling the strength of L2 regularization. The regularization term is automatically added to the objective function during the training process. Adjusting the `alpha` parameter allows you to control the amount of regularization applied.
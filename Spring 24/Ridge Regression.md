Ridge regression, also known as Tikhonov regularization or [[L2 regularization]], is a [[linear regression]] technique that incorporates a [[penalty term]] based on the squared magnitudes of the model coefficients. This penalty term is added to the [[Linear Regression|original loss function]], aiming to prevent [[overfitting]] and produce a more stable and well-behaved model.

### Ridge Regression Objective Function:

The Ridge regression objective function is defined as follows:

$J(\theta) = \text{Original Loss} + \lambda \sum_{i=1}^{n} \theta_i^2$

Here:
- $J(\theta)$ is the new objective function with Ridge regularization,
- $\text{Original Loss}$ is the loss term from the original linear regression objective function,
- $\lambda$ (lambda) is the regularization parameter,
- $\sum_{i=1}^{n} \theta_i^2$ is the sum of the squared coefficients (excluding the intercept term).

The regularization term penalizes large coefficients, effectively shrinking them towards zero. The strength of the regularization is controlled by the \(\lambda\) parameter. A larger \(\lambda\) leads to stronger regularization, while a smaller \(\lambda\) reduces the impact of regularization.

### Key Points about Ridge Regression:

1. **Shrinkage Effect:**
   - Ridge regression introduces a shrinkage effect on the model coefficients. The penalty term discourages large coefficients, preventing the model from fitting the training data too closely and improving its generalization to new, unseen data.

2. **[[Bias-Variance Trade-Off]]:**
   - Ridge regression is part of the bias-variance trade-off. The penalty term adds a bias to the model, reducing variance and helping to control overfitting.

3. **Applicability:**
   - Ridge regression is particularly useful when dealing with multicollinearity, where predictor variables are highly correlated. It helps stabilize the model and provides more reliable estimates of the coefficients.

4. **Non-Sparsifying:**
   - Unlike Lasso regression (L1 regularization), Ridge regression does not lead to sparsity in the coefficients. It tends to shrink all coefficients towards zero but rarely makes them exactly zero.

### Python Example:

Let's use Ridge regression as an example with scikit-learn:

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

In this example, the `Ridge` regression model from scikit-learn is used with an `alpha` parameter controlling the strength of the Ridge regularization. The `alpha` parameter corresponds to the \(\lambda\) parameter in the objective function. Adjusting the `alpha` parameter allows you to control the amount of regularization applied.
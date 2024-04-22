Regularization is a technique used in machine learning and statistical modeling to prevent [[Overfitting]] and improve the generalization performance of a model. Overfitting occurs when a model learns the training data too well, capturing noise and outliers, but fails to generalize well to new, unseen data. [[Regularization]] introduces a [[Penalty Term]] to the objective function being optimized, discouraging the model from fitting the training data too closely.

### Key Points about Regularization:

1. **Objective Function:**
   - Regularization is applied by adding a [[Penalty Term|penalty term]] to the objective function that the model is trying to minimize. The objective function typically consists of two terms: the original loss term (e.g., mean squared error for regression) and a regularization term.

2. **Types of Regularization:**
   - There are different types of regularization commonly used in machine learning:
     - **L1 Regularization (Lasso):** Adds the absolute values of the coefficients to the objective function.
     - **[[L2 Regularization]] (Ridge):** Adds the squared values of the coefficients to the objective function.
     - **Elastic Net:** Combines both L1 and [[L2 Regularization]].

3. **Regularization Parameter (Lambda):**
   - The strength of the regularization is controlled by a hyperparameter often denoted as \( \lambda \) (lambda). The larger the value of \( \lambda \), the stronger the regularization effect. The choice of \( \lambda \) is a trade-off between fitting the training data well and avoiding overfitting.

4. **Effect on Coefficients:**
   - Regularization penalizes large values of the model coefficients. This encourages the model to prefer simpler models with smaller coefficients, which can lead to better generalization.

5. **[[Bias-Variance Trade-Off]]:**
   - Regularization is a part of the bias-variance trade-off. By penalizing complexity, it helps control overfitting, reducing variance but potentially increasing bias. The goal is to find the right balance that minimizes both training and test error.

6. **[[Regularization]] in Different Models:**
   - Regularization is commonly used in linear regression, logistic regression, support vector machines, and neural networks. In neural networks, dropout is also considered a form of regularization.

### L1 and L2 Regularization Formulas:

1. **[[L1 Regularization]] (Lasso):**
   - Objective Function: \( J(\theta) = \text{Original Loss} + \lambda \sum_{i=1}^{n} | \theta_i | \)
   - The regularization term adds the absolute values of the coefficients.

2. **[[L2 Regularization]] (Ridge):**
   - Objective Function: $J(\theta) = \text{Original Loss} + \lambda \sum_{i=1}^{n} \theta_i^2$
   - The regularization term adds the squared values of the coefficients.

### Python Example:

Let's use a simple linear regression example with L2 regularization (Ridge) using scikit-learn:

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

In this example, the Ridge regression model is trained with an additional regularization term (L2 regularization). The regularization strength is controlled by the hyperparameter `alpha`. Adjusting the value of `alpha` allows you to control the regularization effect and find an appropriate trade-off. Regularization is especially beneficial when dealing with high-dimensional datasets or when the number of features exceeds the number of training samples.
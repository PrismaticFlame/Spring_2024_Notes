[[Logistic Regression]] is a popular statistical method used for binary classification tasks, where the goal is to predict the probability of an event occurring or not occurring. [[Maximum Likelihood Estimate|Maximum Likelihood Estimation]] (MLE) is commonly used to estimate the parameters of the logistic regression model.

### Logistic Regression Model:

In logistic regression, the relationship between the input features \(X\) and the binary target variable \(Y\) is modeled using the logistic function (also known as the sigmoid function):

$P(Y=1 | X) = \frac{1}{1 + e^{-(\beta_0 + \beta_1 X_1 + \beta_2 X_2 + ... + \beta_p X_p)}}$

Here:
- $P(Y=1 | X)$ is the probability that \(Y\) equals 1 given the input features \(X\),
- $\beta_0, \beta_1, \beta_2, ..., \beta_p$ are the coefficients (parameters) of the model,
- $X_1, X_2, ..., X_p$ are the input features,
- $e$ is the base of the natural logarithm.

The logistic function ensures that the predicted probabilities lie between 0 and 1, suitable for binary classification.

### Maximum Likelihood Estimation (MLE) for Logistic Regression:

The parameters $\beta_0, \beta_1, \beta_2, ..., \beta_p$ of the logistic regression model are estimated using Maximum Likelihood Estimation (MLE). Given a set of observed data $(x_1, y_1), (x_2, y_2), ..., (x_n, y_n)$, where $x_i$ represents the input features and $y_i$ represents the binary target variable (0 or 1), the likelihood function for logistic regression is defined as:

$L(\beta | X, Y) = \prod_{i=1}^{n} P(Y=y_i | X=x_i)$

To simplify calculations and avoid numerical issues, it is common to work with the log-likelihood function:

$\ell(\beta | X, Y) = \sum_{i=1}^{n} \log P(Y=y_i | X=x_i)$

The goal of MLE is to find the values of $\beta_0, \beta_1, \beta_2, ..., \beta_p$ that maximize the log-likelihood function. This is typically done using optimization algorithms such as gradient descent or Newton's method.

### Optimization:

To optimize the log-likelihood function, the gradients (partial derivatives) of the log-likelihood with respect to each parameter \( \beta_j \) are computed. Then, an optimization algorithm is used to iteratively update the parameter values in the direction that maximizes the log-likelihood.

### Python Example:

Here's a simplified example of logistic regression with MLE using Python and scikit-learn:

```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
import numpy as np

# Load the Iris dataset (binary classification)
iris = load_iris()
X = iris.data[:, :2]  # Select only the first two features
y = (iris.target == 0).astype(int)  # Convert target to binary (1 if Iris Setosa, 0 otherwise)

# Split the data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Create and fit logistic regression model
model = LogisticRegression()
model.fit(X_train, y_train)

# Print coefficients and intercept
print("Coefficients:", model.coef_)
print("Intercept:", model.intercept_)

# Predict probabilities and evaluate performance
y_pred_proba = model.predict_proba(X_test)[:, 1]  # Probability of class 1
```

In this example, we use scikit-learn's logistic regression implementation to fit a logistic regression model to the Iris dataset. The model's coefficients and intercept are estimated using Maximum Likelihood Estimation. The model is then used to predict probabilities for the test set.
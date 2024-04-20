Underfitting is a phenomenon that occurs when a machine learning model is too simple to capture the underlying patterns in the training data. As a result, the model performs poorly not only on the training set but also on new, unseen data. Underfitting is characterized by high bias and low variance. It indicates that the model lacks the complexity needed to represent the true relationship in the data.

### Key Characteristics of Underfitting:

1. **High Bias:**
   - Underfit models have high bias, meaning they make strong assumptions about the data that may not be accurate.
   - These models are often too simplistic to capture the complexities present in the underlying data.

2. **Poor Performance on Training Data:**
   - Underfit models struggle to fit the training data well.
   - They may produce predictions that are consistently off from the true values in the training set.

3. **Poor Generalization to Test Data:**
   - Underfit models generalize poorly to new, unseen data.
   - The lack of complexity and adaptability makes them perform poorly on data they haven't seen during training.

4. **Low Model Complexity:**
   - Underfit models are typically too simple or have too few parameters to represent the underlying relationships in the data.

5. **Examples of Underfitting:**
   - Using a linear model to fit a non-linear relationship in the data.
   - Employing a low-order polynomial to model a high-degree polynomial relationship.

### Causes of Underfitting:

1. **Model Complexity:**
   - Models with insufficient complexity may fail to capture the true patterns in the data.

2. **Feature Selection:**
   - If important features are excluded or the model does not have enough features to represent the underlying relationships, underfitting can occur.

3. **Training Duration:**
   - Insufficient training time or a lack of iterations in the learning process may result in underfitting.

### How to Address Underfitting:

1. **Increase Model Complexity:**
   - Consider using more complex models that can better capture the underlying patterns in the data.

2. **Feature Engineering:**
   - Introduce new features or consider transforming existing features to provide the model with more information.

3. **Hyperparameter Tuning:**
   - Adjust hyperparameters, such as the learning rate or regularization strength, to find a better balance between bias and variance.

4. **Ensemble Methods:**
   - Use ensemble methods like Random Forests or Gradient Boosted Trees to combine predictions from multiple models and reduce underfitting.

5. **Model Selection:**
   - Choose a more sophisticated model architecture that can handle the complexity of the underlying relationships in the data.

6. **Increase Training Duration:**
   - Train the model for a longer duration, allowing it to learn more from the data.

### Example (Python - Scikit-Learn):

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
import numpy as np

# Assuming X_train, y_train, X_test, y_test are your training and test data
# Linear Regression Model (Example of a simple model)
model = LinearRegression()

# Train the model
model.fit(X_train, y_train)

# Predict on training and test sets
y_train_pred = model.predict(X_train)
y_test_pred = model.predict(X_test)

# Calculate Mean Squared Error (MSE) as a performance metric
train_mse = mean_squared_error(y_train, y_train_pred)
test_mse = mean_squared_error(y_test, y_test_pred)

print("Training MSE:", train_mse)
print("Test MSE:", test_mse)
```

In this example, a linear regression model is used, which is a simple model. If the relationship between features and the target variable is more complex, this model may underfit the data.

Addressing underfitting often involves experimenting with more complex models, introducing additional features, or adjusting hyperparameters to achieve a better fit to the training data and improve generalization to new data.


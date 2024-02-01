**Mean Squared Error (MSE)** is a common metric used to evaluate the performance of a regression model. It measures the average squared difference between the predicted values and the actual values. The goal is to minimize the MSE to have a more accurate model.

### Definition:

For a dataset with \(m\) observations, where \(y_i\) is the actual value and \(\hat{y}_i\) is the predicted value for the \(i\)-th observation, the Mean Squared Error is calculated as follows:

$\text{MSE} = \frac{1}{m} \sum_{i=1}^{m} (y_i - \hat{y}_i)^2$

### Explanation:

1. **Squared Differences:**
   - For each observation, calculate the squared difference between the actual (\(y_i\)) and predicted (\(\hat{y}_i\)) values.

2. **Average:**
   - Take the average (mean) of all the squared differences.

3. **Higher Weight for Larger Errors:**
   - Squaring the differences gives higher weight to larger errors, making the metric sensitive to outliers.

4. **Units of Measurement:**
   - The units of MSE are the square of the units of the dependent variable, making it interpretable in the same units as the variable being predicted.

### Interpretation:

- A lower MSE indicates better model performance, as it means that, on average, the model's predictions are closer to the actual values.
- MSE penalizes larger errors more severely than smaller errors, which is desirable in many regression scenarios.

### Example:

Consider a simple dataset with three observations:

Actual Values (\(y\)):  \([2, 4, 7]\)

Predicted Values (\(\hat{y}\)): \([3, 3, 6]\)

1. Squared Differences:

   $(2-3)^2 = 1, \quad (4-3)^2 = 1, \quad (7-6)^2 = 1$

2. Average:

   $\text{MSE} = \frac{1}{3} \times (1 + 1 + 1) = 1$

In this example, the Mean Squared Error is 1, indicating that, on average, the squared difference between the actual and predicted values is 1.

### Python Example (using Scikit-Learn):

```python
from sklearn.metrics import mean_squared_error

# Actual values
y_actual = [2, 4, 7]

# Predicted values
y_pred = [3, 3, 6]

# Calculate Mean Squared Error
mse = mean_squared_error(y_actual, y_pred)

print("Mean Squared Error:", mse)
```

In this Python example, the `mean_squared_error` function from Scikit-Learn is used to calculate the MSE for the provided actual and predicted values. The result will be the Mean Squared Error for the regression model on this particular dataset.
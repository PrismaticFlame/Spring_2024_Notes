Z scaling, also known as standardization or z-score normalization, is a common preprocessing technique in statistics and machine learning. It involves transforming a variable's values so that they have a mean of 0 and a standard deviation of 1. This transformation is applied to make the variables comparable and to give them a similar scale, which can be important for certain algorithms and analyses.

The formula for z scaling is given by:

$$z = \frac{{x - \mu}}{{\sigma}}$$

Here:
- $z$ is the standardized value,
- $x$ is the original value,
- $\mu$ is the mean (average) of the variable,
- $\sigma$ is the standard deviation of the variable.

### Key Points about Z Scaling:

1. **Mean Centering:**
   - Z scaling involves subtracting the mean of the variable from each data point. This results in the variable being "mean-centered" around 0.

2. **Scaling:**
   - After mean centering, the values are divided by the standard deviation of the variable. This step scales the variable, ensuring that it has a standard deviation of 1.

3. **Interpretability:**
   - Z scaling does not change the shape of the distribution of the variable; it only shifts and scales it. This makes it particularly useful when interpretability of the original values is important.

4. **Applicability:**
   - Z scaling is commonly applied in situations where the scale of the variables is different, and it is important to give them a comparable scale. This is often the case in machine learning algorithms that are sensitive to the scale of features, such as gradient-based optimization methods.

### Python Example:

Here is a simple Python example using the scikit-learn library to demonstrate z scaling:

```python
from sklearn.preprocessing import StandardScaler
import numpy as np

# Generate example data
data = np.array([[1, 2, 3],
                 [4, 5, 6],
                 [7, 8, 9]])

# Create a StandardScaler object
scaler = StandardScaler()

# Fit the scaler to the data and transform the data
scaled_data = scaler.fit_transform(data)

print("Original Data:")
print(data)
print("\nScaled Data (Z Scores):")
print(scaled_data)
```

In this example, the `StandardScaler` from scikit-learn is used to z scale the data. The resulting `scaled_data` will have a mean of 0 and a standard deviation of 1 for each variable.
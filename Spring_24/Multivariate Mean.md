---
aliases:
  - Multivariate Mean
  - Gaussian Distribution
  - Multivariate Gaussian Distribution
---
Certainly! The multivariate mean, often denoted as \(\boldsymbol{\mu}\), represents the average values of each variable in a multivariate dataset. It is a vector that captures the central tendency of the data in multiple dimensions. For a \(p\)-dimensional dataset, the multivariate mean is a \(p\)-dimensional vector.

### Multivariate Mean Calculation:

Given a dataset with \(n\) observations, each having \(p\) variables, the multivariate mean for each variable \(X_i\) is calculated as the average of the corresponding values across all observations. The multivariate mean vector \(\boldsymbol{\mu}\) is formed by collecting the means for each variable.

The formula for the mean of a variable \(X_i\) in a dataset is given by:

\[ \mu_i = \frac{1}{n} \sum_{j=1}^{n} x_{ij} \]

Here:
- \( \mu_i \) is the mean of variable \(X_i\).
- \( x_{ij} \) is the value of variable \(X_i\) for the \(j\)-th observation.
- \( n \) is the number of observations.

The multivariate mean vector \(\boldsymbol{\mu}\) is then formed by collecting the means for all \(p\) variables:

\[ \boldsymbol{\mu} = [\mu_1, \mu_2, \ldots, \mu_p] \]

### Python Example:

Let's consider a simple example where we have a 3-dimensional dataset:

```python
import numpy as np

# Sample 3D dataset with 4 observations
data = np.array([[1, 2, 3],
                 [4, 5, 6],
                 [7, 8, 9],
                 [10, 11, 12]])

# Calculate multivariate mean
multivariate_mean = np.mean(data, axis=0)

print("Multivariate Mean:")
print(multivariate_mean)
```

In this example:
- The dataset `data` has 4 observations and 3 variables.
- The `np.mean` function is used to calculate the mean along each dimension (`axis=0` means along the rows, i.e., variable-wise mean).
- The resulting `multivariate_mean` vector contains the means for each variable.

The output would be:

```
Multivariate Mean:
[5.5 6.5 7.5]
```

This means that the mean of the first variable is 5.5, the mean of the second variable is 6.5, and the mean of the third variable is 7.5. The multivariate mean vector captures the central tendencies of the dataset across all dimensions.
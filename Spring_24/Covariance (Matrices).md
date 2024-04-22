---
aliases:
  - Covariance
  - Multivariate Gaussian Distribution
  - Gaussian Distribution
  - Covariance Matrix
---
Certainly! Covariance is a measure that quantifies the degree to which two variables change together. In the context of multivariate datasets, covariance provides insights into how pairs of variables vary jointly. The covariance between two variables, \(X\) and \(Y\), is calculated as the average of the product of their deviations from their respective means.

### Covariance between Two Variables:

For two variables \(X\) and \(Y\), the covariance (\(\text{cov}(X, Y)\)) is given by:

\[ \text{cov}(X, Y) = \frac{1}{n} \sum_{i=1}^{n} (X_i - \mu_X)(Y_i - \mu_Y) \]

Here:
- \(n\) is the number of observations.
- \(X_i\) and \(Y_i\) are the values of variables \(X\) and \(Y\) for the \(i\)-th observation.
- \(\mu_X\) and \(\mu_Y\) are the means of variables \(X\) and \(Y\), respectively.

### Covariance Matrix:

In a multivariate context, the covariance matrix is a symmetric matrix that summarizes the covariances between all pairs of variables in a dataset. If we have \(p\) variables, the covariance matrix (\(\Sigma\)) is a \(p \times p\) matrix, and the element in the \(i\)-th row and \(j\)-th column represents the covariance between variables \(X_i\) and \(X_j\).

The covariance matrix is calculated as follows:

\[ \Sigma = \frac{1}{n} \sum_{i=1}^{n} (\mathbf{x}_i - \boldsymbol{\mu})(\mathbf{x}_i - \boldsymbol{\mu})^T \]

Here:
- \(\mathbf{x}_i\) is the \(i\)-th observation, represented as a column vector.
- \(\boldsymbol{\mu}\) is the mean vector of the variables.

The diagonal elements of the covariance matrix represent the variances of individual variables, and the off-diagonal elements represent the covariances between variable pairs.

### Python Example:

Let's consider a simple example with a 3-dimensional dataset:

```python
import numpy as np

# Sample 3D dataset with 4 observations
data = np.array([[1, 2, 3],
                 [4, 5, 6],
                 [7, 8, 9],
                 [10, 11, 12]])

# Calculate covariance matrix
covariance_matrix = np.cov(data, rowvar=False)

print("Covariance Matrix:")
print(covariance_matrix)
```

In this example:
- The `np.cov` function is used to calculate the covariance matrix.
- `rowvar=False` indicates that each column represents a variable, and each row is an observation.
- The resulting `covariance_matrix` is a 3x3 matrix.

The output would be:

```
Covariance Matrix:
[[10.66666667 10.66666667 10.66666667]
 [10.66666667 10.66666667 10.66666667]
 [10.66666667 10.66666667 10.66666667]]
```

This covariance matrix shows the covariances between all pairs of variables. The diagonal elements represent the variances of individual variables, and the off-diagonal elements represent the covariances between variable pairs. In this case, all covariances are the same because the data is generated to have a simple pattern.

# Independence
Two features are independent if they have a covariance of 0
- This means there is no relationship between them
- Two different dice rolled are independent
- If we think of features as dimensions, we want features to be independent to maximize the descriptiveness of the data

- Statisticians often assume features are independent, however this is rarely true
	- It greatly simplifies models, and models are just approximations of the real world

# Mahalanobis Distance
Similarly, we can redefine distance which takes covariance into account
- **Mahalanobis Distance** ($D_m$)
	- Distance with respect to the covariance in the data
	- Given points represented as vectors a and b, and $\Sigma$, the covariance matrix
	- With a covariance matrix = identity matrix, this reduces to the Euclidean distance
$$d_m = \sqrt{(a-b)^T\Sigma^{-1}(a-b)}$$
This is Euclidean distance scaled by covariance (more obvious for a single dimension)

For one dimensional values a and b: $$D_M = \sqrt{(a-b)^T\Sigma^{-1}(a-b)} = \sqrt{\frac{(a-b)^2}{\sigma}}$$

---
aliases:
  - Gaussian Distribution
  - Multivariate Gaussian Distribution
---
Certainly! The multivariate Gaussian distribution, also known as the multivariate normal distribution, is a generalization of the univariate (single-variable) Gaussian distribution to multiple variables. It is often used to model the joint probability distribution of a set of continuous random variables.

### Multivariate Gaussian Distribution:

#### Probability Density Function (PDF):
The probability density function of a multivariate Gaussian distribution with mean vector ($\boldsymbol{\mu}$) and covariance matrix ($\Sigma$) for a ($p$)-dimensional random vector ($\mathbf{X} = [X_1, X_2, \ldots, X_p]$) is given by:

$f(\mathbf{x}) = \frac{1}{(2\pi)^{p/2} \sqrt{\text{det}(\Sigma)}} \exp\left(-\frac{1}{2} (\mathbf{x} - \boldsymbol{\mu})^T \Sigma^{-1} (\mathbf{x} - \boldsymbol{\mu})\right)$

Here:
- ($\mathbf{x}$) is a ($p$)-dimensional vector representing a specific point in the space.
- ($\boldsymbol{\mu}$) is the mean vector.
- ($\Sigma$) is the covariance matrix.
- ($\text{det}(\Sigma)$) is the determinant of the covariance matrix.
- ($\Sigma^{-1}$) is the inverse of the covariance matrix.

#### Example Problems:

**Problem 1:**
Consider a bivariate (2D) Gaussian distribution with mean vector \(\boldsymbol{\mu} = [1, 2]\) and covariance matrix \(\Sigma = \begin{bmatrix} 2 & 1 \\ 1 & 3 \end{bmatrix}\). Compute the probability density function at the point \(\mathbf{x} = [3, 4]\).

**Solution:**
\[ f(\mathbf{x}) = \frac{1}{2\pi \sqrt{\text{det}(\Sigma)}} \exp\left(-\frac{1}{2} (\mathbf{x} - \boldsymbol{\mu})^T \Sigma^{-1} (\mathbf{x} - \boldsymbol{\mu})\right) \]

**Python Code:**
```python
import numpy as np
from scipy.stats import multivariate_normal

# Parameters
mean_vector = np.array([1, 2])
covariance_matrix = np.array([[2, 1], [1, 3]])
point = np.array([3, 4])

# Multivariate Gaussian PDF
mvn = multivariate_normal(mean=mean_vector, cov=covariance_matrix)
pdf_value = mvn.pdf(point)

print(f'Probability Density at {point}: {pdf_value:.4e}')
```

**Problem 2:**
Generate random samples from a trivariate (3D) Gaussian distribution with mean vector \(\boldsymbol{\mu} = [0, 0, 0]\) and covariance matrix \(\Sigma = \begin{bmatrix} 1 & 0.5 & 0 \\ 0.5 & 2 & 0.5 \\ 0 & 0.5 & 3 \end{bmatrix}\).

**Solution:**
```python
# Parameters
mean_vector_3d = np.array([0, 0, 0])
covariance_matrix_3d = np.array([[1, 0.5, 0], [0.5, 2, 0.5], [0, 0.5, 3]])

# Generate random samples
num_samples = 1000
samples = np.random.multivariate_normal(mean_vector_3d, covariance_matrix_3d, num_samples)

# Display samples
print('Generated Samples:')
print(samples[:5, :])  # Displaying the first 5 samples
```

These examples demonstrate basic computations with the multivariate Gaussian distribution, including calculating the probability density at a specific point and generating random samples. The calculations and code make use of the mean vector, covariance matrix, and the probability density function of the multivariate Gaussian distribution.


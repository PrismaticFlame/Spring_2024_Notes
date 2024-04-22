In quantum mechanics, normalization is a mathematical requirement imposed on wave functions to ensure that the probability interpretation is consistent. A normalized wave function is one that satisfies the condition that the total probability of finding the system is equal to 1 when integrated over all possible positions.

Mathematically, for a one-dimensional wave function $\Psi(x)$, the normalization condition is expressed as:

$\int_{-\infty}^{\infty} |\Psi(x)|^2 \, dx = 1$

For three-dimensional wave functions $\Psi(\mathbf{r})$ (where $\mathbf{r}$ is a position vector), the normalization condition becomes:

$\int |\Psi(\mathbf{r})|^2 \, d\mathbf{r} = 1$

Normalization ensures that the probability density $|\Psi(x)|^2$ or $|\Psi(\mathbf{r})|^2$ integrates to 1 over all possible positions, representing the certainty that the particle is somewhere in space.

Now, let's look at two examples of normalized wave functions:

### Example 1: Normalized Gaussian Wave Function

Consider a one-dimensional Gaussian wave function given by:

$\Psi(x) = \frac{1}{\pi^{1/4} \sqrt{2^n n!}} e^{-x^2/2}$

where $n$ is a positive integer.

To check normalization, you need to integrate $|\Psi(x)|^2$ over all $x$:

$\int_{-\infty}^{\infty} \left| \frac{1}{\pi^{1/4} \sqrt{2^n n!}} e^{-x^2/2} \right|^2 \, dx$

If this integral equals 1, the wave function is normalized.

### Example 2: Normalized Particle in a Box Wave Function

Consider a particle in a one-dimensional box of length $L$. The normalized wave function for the particle in the ground state (n = 1) is given by:

$\Psi(x) = \sqrt{\frac{2}{L}} \sin\left(\frac{\pi x}{L}\right)$

The normalization condition for this wave function is:

$\int_{0}^{L} \left| \sqrt{\frac{2}{L}} \sin\left(\frac{\pi x}{L}\right) \right|^2 \, dx$

If this integral equals 1, the wave function is normalized.

In both examples, the goal is to evaluate the integral representing the probability density and confirm that it equals 1. If the integral is 1, the wave function is normalized and satisfies the probabilistic interpretation in quantum mechanics.
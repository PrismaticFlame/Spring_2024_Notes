The infinite square well, also known as the particle in a box, is a simple yet fundamental model in quantum mechanics that helps illustrate key principles of quantum theory. This model describes a particle confined within an infinite potential well, resulting in quantized energy levels and wave functions.

### Potential Energy Profile:

The potential energy ($V(x)$) in the infinite square well is given by:

$V(x) = \begin{cases} 0 & \text{for } 0 < x < L \\\infty & \text{otherwise}\end{cases}$

In other words, the particle is free to move between $0$ and $L$, and its potential energy is infinite outside this region.

### [[Time Independent Schrodinger Equation|Time-Independent Schrödinger Equation]] (TISE):

The time-independent Schrödinger equation for the infinite square well is:

$-\frac{\hbar^2}{2m} \frac{d^2 \psi(x)}{dx^2} = E \psi(x)$

Here:
- $\psi(x)$ is the spatial wave function.
- $m$ is the mass of the particle.
- $E$  is the energy eigenvalue.

### Solution of TISE:

The solution to the TISE is obtained by solving the differential equation within the boundaries of the well ($0 < x < L$) and applying boundary conditions. The general form of the solution is given by:

$\psi_n(x) = \sqrt{\frac{2}{L}} \sin\left(\frac{n\pi x}{L}\right)$

Here:
- $n$ is a positive integer, representing the quantum number.
- $L$ is the width of the well.

### Energy Levels:

The energy levels ($E_n$) corresponding to each wave function are quantized and given by:

$E_n = \frac{n^2 \pi^2 \hbar^2}{2mL^2}$

Here:
- $n$ is the quantum number.

The energy levels are spaced evenly, reflecting the quantization of energy in the well.

### Probability Density:

The probability density ($|\psi_n(x)|^2$) for the particle's position in the $n$-th energy level is given by:

$$|\psi_n(x)|^2 = \frac{2}{L} \sin^2\left(\frac{n\pi x}{L}\right)$$

The probability density shows regions of high and low probability of finding the particle within the well.

### Key Concepts and Observations:

1. **Quantization of Energy:**
   - The energy levels are quantized and depend on the quantum number \(n\). Higher energy levels have more oscillations in the wave function.

2. **Orthogonality:**
   - Different wave functions corresponding to different energy levels are orthogonal: $\int_{0}^{L} \psi_m^*(x) \psi_n(x) \,dx = \delta_{mn}$, where $\delta_{mn}$ is the Kronecker delta.

3. **Probability Density:**
   - The probability density exhibits nodal patterns, regions with zero probability, and peaks where the particle is more likely to be found.

4. **Tunneling:**
   - The infinite square well serves as a simple model for understanding quantum tunneling, as the particle cannot exist outside the well due to the infinite potential barrier.

The infinite square well provides a foundation for understanding more complex quantum systems and is often used as a starting point for introducing the principles of quantization and wave-particle duality.

![[Pasted image 20240130190619.png]]



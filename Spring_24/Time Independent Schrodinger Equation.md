Certainly! The Time-Independent Schrödinger Equation (TISE) is a fundamental equation in quantum mechanics that describes the behavior of non-relativistic particles in a conservative potential. It provides the relationship between the spatial wave function of a quantum system and its energy.

The TISE is given by:

$$\hat{H} \Psi(\mathbf{r}) = E \Psi(\mathbf{r})$$

Here:
- $\hat{H}$ is the [[Hamiltonian]] operator, representing the total energy of the system.
- $\Psi(\mathbf{r})$ is the spatial wave function, which depends on the spatial coordinates $( \mathbf{r} )$ of the particle.
- $E$ is the energy eigenvalue associated with the particular state described by $\Psi(\mathbf{r})$.

The TISE essentially states that the Hamiltonian operator acting on the wave function gives back the same wave function multiplied by the energy eigenvalue. Solving the TISE allows one to determine the allowed energy levels and corresponding wave functions of a quantum system.

### Example 1: Particle in a Box

Consider a one-dimensional particle in a box of length $L$. The potential energy inside the box is zero, and outside the box, it is infinite. The TISE for this system is:

$$-\frac{\hbar^2}{2m} \frac{d^2 \psi(x)}{dx^2} = E \psi(x)$$

The solution to this equation gives the quantized energy levels and corresponding wave functions for the particle in the box.

### Example 2: Harmonic Oscillator

The TISE for a one-dimensional harmonic oscillator with mass $m$ and spring constant $k$ is given by:

$$-\frac{\hbar^2}{2m} \frac{d^2 \psi(x)}{dx^2} + \frac{1}{2}kx^2 \psi(x) = E \psi(x)$$

This equation describes the energy levels and wave functions for a particle in a harmonic potential.

### Example 3: Hydrogen Atom

For a hydrogen atom, the TISE in spherical coordinates ( $r, \theta, \phi$ ) is given by:

$$-\frac{\hbar^2}{2\mu} \nabla^2 \psi(\mathbf{r}) - \frac{e^2}{r} \psi(\mathbf{r}) = E \psi(\mathbf{r})$$

Here:
- $\mu$ is the reduced mass of the electron and proton.
- $e$ is the elementary charge.
- $\nabla^2$ is the Laplacian operator.

This equation describes the energy levels and wave functions for the electron in a hydrogen atom.

### Solving the TISE:

Solving the TISE typically involves finding the wave function $\Psi(\mathbf{r})$ and the corresponding energy eigenvalues $E$. The solutions depend on the specific potential energy term in the Hamiltonian. Techniques such as separation of variables, series expansions, and numerical methods are often employed to find solutions.

In summary, the Time-Independent Schrödinger Equation is a key equation in quantum mechanics that governs the energy levels and wave functions of quantum systems. Solving the TISE provides insights into the quantized nature of energy in quantum systems. Examples include the particle in a box, harmonic oscillator, and hydrogen atom.
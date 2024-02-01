Stationary states are important concepts in quantum mechanics, describing certain solutions to the time-dependent Schrödinger equation (TDSE). These states have unique properties that make them particularly interesting and useful in the understanding of quantum systems.

### Time-Dependent Schrödinger Equation (TDSE):

The time-dependent Schrödinger equation is given by:

$$i\hbar \frac{\partial}{\partial t} \Psi(\mathbf{r}, t) = \hat{H} \Psi(\mathbf{r}, t)$$

Here:
- $\Psi(\mathbf{r}, t)$ is the wave function of the quantum system.
- $\hat{H}$ is the Hamiltonian operator, representing the total energy of the system.
- $\hbar$ is the reduced Planck constant.

### Stationary States:

A stationary state is a special solution to the TDSE where the time dependence of the wave function is a simple phase factor. Mathematically, a stationary state is represented as:

$$\Psi(\mathbf{r}, t) = \psi(\mathbf{r}) e^{-iEt/\hbar}$$

Here:
- $\psi(\mathbf{r})$ is the spatial part of the [[wave function]], representing the stationary spatial distribution.
- $E$ is the energy eigenvalue associated with that state.

### Properties of Stationary States:

1. **Time Independence:**
   - In a stationary state, the probability density $|\Psi(\mathbf{r}, t)|^2$ is time-independent. This is because the time-dependent part is a phase factor that cancels out when squared.

2. **Energy Eigenstate:**
   - Stationary states are energy eigenstates, meaning that the measurement of energy in such a state will always yield a specific value $E$.

3. **Orthogonality:**
   - Different stationary states corresponding to distinct energy eigenvalues are orthogonal to each other. Mathematically, if $\Psi_n(\mathbf{r}, t)$ and $\Psi_m(\mathbf{r}, t)$ are stationary states with energies $E_n$ and $E_m$ (where $n \neq m$ ), then $\langle \Psi_n | \Psi_m \rangle = 0$.

4. **Completeness:**
   - The set of stationary states can form a complete basis for the Hilbert space, meaning that any wave function can be expressed as a superposition of these stationary states.

5. **Eigenstates of the [[Hamiltonian]]:**
   - Stationary states are eigenstates of the Hamiltonian operator: $\hat{H} \Psi(\mathbf{r}, t) = E \Psi(\mathbf{r}, t)$.

### Application:

Stationary states are particularly useful in simplifying the analysis of quantum systems. When a system is in a stationary state, the time evolution is straightforward, and measurable quantities such as energy can be predicted with certainty. For example, in the context of the particle in a box, the stationary states are the standing waves that represent quantized energy levels.

In summary, stationary states in quantum mechanics are solutions to the time-dependent Schrödinger equation where the time dependence is a simple phase factor. These states are characterized by time-independent probability densities, specific energy values, orthogonality, and completeness. They provide a convenient basis for understanding and solving quantum mechanical problems.
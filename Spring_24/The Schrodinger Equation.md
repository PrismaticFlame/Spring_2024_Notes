The Schrödinger Equation is a fundamental equation in quantum mechanics that describes how the quantum state of a physical system changes over time. It was formulated by Austrian physicist Erwin Schrödinger in 1925. The equation is used to determine the wave function, which contains information about the probability amplitude of finding a particle in a particular state.

Here is the [[Time Independent Schrodinger Equation|time-dependent Schrödinger Equation]]:

$$i\hbar \frac{\partial \Psi}{\partial t} = \hat{H} \Psi$$

- ( $i$ ) is the imaginary unit.
- ( $\hbar$ ) is the reduced Planck constant.
- ($\frac{\partial \Psi}{\partial t}$) is the partial derivative of the wave function with respect to time.
- ($\hat{H}$) is the [[Hamiltonian]] operator.
- ( $\Psi$ ) is the [[Wave Function]].

The time-independent Schrödinger Equation, which is often used when the Hamiltonian is not explicitly time-dependent, is:

$$\hat{H} \Psi = E \Psi$$

- ( $E$ ) represents the energy eigenvalue of the system.

Now, let's break down the components:

1. **Wave Function (\( $\Psi$ \)):**
   - The wave function is a mathematical function that describes the quantum state of a system. It contains information about the position, momentum, and other physical properties of particles.

2. **Hamiltonian Operator (\( $\hat{H}$ \)):**
   - The Hamiltonian operator represents the total energy of a system. It includes kinetic and potential energy terms and is a mathematical operator acting on the wave function.

3. **Energy Eigenvalue (\( $E$ \)):**
   - The solutions to the Schrödinger Equation provide the possible energy states of the system. These are the eigenvalues of the Hamiltonian operator.

4. **Time Dependence:**
   - In the time-dependent Schrödinger Equation, the term ( $i\hbar \frac{\partial \Psi}{\partial t}$ ) accounts for the evolution of the wave function over time.

### Example:
Consider a particle in a one-dimensional box with no external forces. The potential energy is zero within the box and infinite outside. The Hamiltonian operator for this system is:

$$\hat{H} = -\frac{\hbar^2}{2m} \frac{d^2}{dx^2} + V(x)$$

where ( $m$ ) is the mass of the particle, ( $\hbar$ ) is the reduced Planck constant, ( $\frac{d^2}{dx^2}$ ) is the second derivative with respect to position, and ( $V(x)$ ) is the potential energy function.

The time-dependent Schrödinger Equation for this system is:

$$i\hbar \frac{\partial \Psi(x, t)}{\partial t} = -\frac{\hbar^2}{2m} \frac{\partial^2 \Psi(x, t)}{\partial x^2} + V(x) \Psi(x, t)$$

Solving this equation provides the wave function \( \Psi(x, t) \), which describes the probability distribution of finding the particle at a certain position \( x \) and time \( t \) within the box. The eigenvalues of the Hamiltonian operator correspond to the allowed energy levels of the particle in the box.
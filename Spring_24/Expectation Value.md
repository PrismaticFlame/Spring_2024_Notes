In quantum mechanics, an expectation value, also known as an expectation or expected value, is a statistical measure that provides the average value of a physical quantity in a given quantum state. It is a way of quantifying the most likely or expected outcome of a measurement, based on the probabilities associated with different possible outcomes.

The expectation value of an observable $A$ in a quantum state described by the wave function $\Psi$ is denoted as $\langle A \rangle$ and is given by the expression:

$\langle A \rangle = \int \Psi^*(\mathbf{r}, t) \hat{A} \Psi(\mathbf{r}, t) \, d\mathbf{r}$

Here, $\hat{A}$ is the operator corresponding to the observable \( A \), $\Psi^*(\mathbf{r}, t)$ is the complex conjugate of the wave function, $\Psi(\mathbf{r}, t)$, and the integration is performed over all possible positions ($\mathbf{r}$).

Key points about expectation values in quantum mechanics:

1. **Physical Interpretation:**
   - The expectation value represents the average value that would be obtained if the measurement of the observable \( A \) is repeated many times on identical systems prepared in the same quantum state described by \( \Psi \).

2. **Operators and Observables:**
   - Observables in quantum mechanics, such as position ($\hat{x}$), momentum ($\hat{p}$), energy ($\hat{H}$), and angular momentum ($\hat{L}$), are represented by operators. The expectation value involves the application of these operators to the wave function.

3. **Eigenstates and Eigenvalues:**
   - When the system is in an eigenstate of an observable $A$, the expectation value $\langle A \rangle$ is equal to the corresponding eigenvalue. Mathematically:
     $\langle A \rangle = \langle \psi | \hat{A} | \psi \rangle = a_n$
     where $| \psi \rangle$ is an eigenstate of $\hat{A}$ with eigenvalue  $a_n$.

4. **Time Evolution:**
   - The expectation value may depend on time if the wave function evolves over time. In that case, the time-dependent expectation value is given by:
     $\langle A \rangle (t) = \int \Psi^*(\mathbf{r}, t) \hat{A} \Psi(\mathbf{r}, t) \, d\mathbf{r}$

5. **Born Rule Connection:**
   - The Born Rule relates the probability density $P$ of obtaining a particular measurement outcome to the square of the magnitude of the wave function $\Psi$:
     $P(\mathbf{r}) = |\Psi(\mathbf{r})|^2$
     The expectation value involves integrating this probability density over all possible positions.

6. **Observable Properties:**
   - The expectation value provides insight into the average behavior of a quantum system. For example, $\langle \hat{x} \rangle$ represents the average position of a particle, $\langle \hat{p} \rangle$ represents the average momentum, and $\langle \hat{H} \rangle$ represents the average energy.

In summary, the expectation value in quantum mechanics is a crucial concept that connects the mathematical formalism of quantum theory with observable properties of physical systems. It provides a way to extract meaningful information about the average behavior of quantum systems based on their wave functions and the operators representing observables.
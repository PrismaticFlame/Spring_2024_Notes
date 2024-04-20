Eigenstates and eigenvalues are fundamental concepts in quantum mechanics. They play a crucial role in the mathematical formulation of quantum theory and are central to understanding the behavior of quantum systems.

### Eigenstates:

An eigenstate of a quantum mechanical operator is a state for which the application of the operator results in the state being multiplied by a scalar, which is called the eigenvalue. Mathematically, if $\hat{O}$ is an operator and $| \psi \rangle$ is a state vector, the eigenstate equation is:

$\hat{O} | \psi \rangle = \lambda | \psi \rangle$

Here:
- $\hat{O}$ is the operator.
- $| \psi \rangle$ is the eigenstate of the operator.
- $\lambda$ is the eigenvalue associated with that eigenstate.

Eigenstates represent states of definite values for the observable represented by the operator. For example, in the context of quantum mechanics, position and momentum operators have sets of eigenstates associated with them.

### Eigenvalues:

Eigenvalues are the possible outcomes of measurements of observables in quantum mechanics. When an observable is measured, the corresponding operator acts on the state vector, and the result is a multiple of the original state vector. The factor by which the state vector is multiplied is the eigenvalue associated with that particular eigenstate.

For example, consider the position operator $\hat{x}$ acting on an eigenstate $| \psi \rangle$:

$\hat{x} | \psi \rangle = x | \psi \rangle$

Here, $x$ is the eigenvalue associated with the eigenstate $| \psi \rangle$, representing the position of the particle in this case.

### Properties of Eigenstates and Eigenvalues:

1. **Completeness:**
   - The set of eigenstates of an operator can form a complete basis for the Hilbert space. This means that any state vector in the space can be expressed as a linear combination of the eigenstates of the operator.

2. **Orthogonality:**
   - Eigenstates corresponding to distinct eigenvalues of a Hermitian operator are orthogonal. Mathematically, if $\hat{O} | \psi_i \rangle = \lambda_i | \psi_i \rangle$ and $\hat{O} | \psi_j \rangle = \lambda_j | \psi_j \rangle$ with $\lambda_i \neq \lambda_j$, then $\langle \psi_i | \psi_j \rangle = 0$.

3. **Hermitian Operators:**
   - Observables in quantum mechanics are represented by Hermitian operators. Hermitian operators have real eigenvalues, and their eigenstates form a complete orthogonal basis.

4. **[[Normalization]]:**
   - Eigenstates are typically normalized, meaning that the inner product of an eigenstate with itself is equal to 1. Mathematically, $\langle \psi_i | \psi_i \rangle = 1$.

### Example:

Consider the momentum operator $\hat{p}$ acting on an eigenstate $| \phi_p \rangle$ associated with the eigenvalue $p$:

$\hat{p} | \phi_p \rangle = p | \phi_p \rangle$

Here, $| \phi_p \rangle$ represents a plane wave with definite momentum  $p$. The eigenvalue $p$ is the momentum of the particle in this state.

In summary, eigenstates and eigenvalues are essential concepts in quantum mechanics. They provide a way to represent and understand the quantized values of physical observables and form the foundation for solving quantum mechanical problems. The mathematics of eigenstates and eigenvalues is crucial for describing the behavior of quantum systems and making predictions about measurement outcomes.
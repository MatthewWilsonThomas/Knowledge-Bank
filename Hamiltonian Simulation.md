#QuantumComputing 
#QuantumMechanics 
#Simulation 


### Problem
In the Hamiltonian simulation problem, given a Hamiltonian $H$ ( $2^n \times 2^n$ hermitian matrix acting on $n$ qubits), a time $t$ and maximum simulation error $\epsilon$, the goal is to find an algorithm that approximates $U$ such that $\left\|U-e^{-i H t}\right\| \leq \epsilon$, where $e^{-i H t}$ is the ideal evolution and $\|\cdot\|$ is the spectral norm. A special case of the Hamiltonian simulation problem is the local Hamiltonian simulation problem. This is when $H$ is a k-local Hamiltonian on $n$ qubits where $H=\sum_{j=1}^m H_j$ and $H_j$ acts non-trivially on at most $k$ qubits instead of $n$ qubits. The local Hamiltonian simulation problem is important because most Hamiltonians that occur in nature are k-local.

### Techniques
#### Product Formulas
Also known as Trotter formulas or Trotter-Suzuki decompositions, Product formulas simulate the sum-of-terms of a Hamiltonian by simulating each one separately for a small time slice. If $H=A+B+C$, then $U=e^{-i(A+B+C) t}=\left(e^{-i A t / r} e^{-i B t / r} e^{-i C t / r}\right)^r$ for a large $r$; where $r$ is the number of time steps to simulate for. The larger the $r$, the more accurate the simulation.
If the Hamiltonian is represented as a Sparse matrix, the distributed edge colouring algorithm can be used to decompose it into a sum of terms; which can then be simulated by a Trotter-Suzuki algorithm.

#### [[Taylor Series]]
$e^{-i H t}=\sum_{n=0}^{\infty} \frac{(-i H t)^n}{n !}=I-i H t-\frac{H^2 t^2}{2}+\frac{i H^3 t^3}{6}+\cdots$ by the Taylor series expansion. This says that during the evolution of a quantum state, the Hamiltonian is applied over and over again to the system with a various number of repetitions. The first term is the identity matrix so the system doesn't change when it is applied, but in the second term the Hamiltonian is applied once. For practical implementations, the series has to be truncated $\left(\sum_{n=0}^N \frac{(-i H t)^n}{n !}\right)$, where the bigger the $N$, the more accurate the simulation. ${ }^{[7]}$ This truncated expansion is then implemented via the linear combination of unitaries (LCU) technique for Hamiltonian simulation. ${ }^{[6]}$ Namely, one decomposes the Hamiltonian $H=\sum_{\ell=1}^L \alpha_{\ell} H_{\ell}$ such that each $H_{\ell}$ is unitary (for instance, the Pauli operators always provide such a basis), and so each $H^n=\sum_{\ell_1, \ldots, \ell_n=1}^L \alpha_{\ell_1} \cdots \alpha_{\ell_n} H_{\ell_1} \cdots H_{\ell_n}$ is also a linear combination of unitaries.

#### Quantum Walk
In the quantum walk, a unitary operation whose spectrum is related to the Hamiltonian is implemented then the Quantum phase estimation algorithm is used to adjust the eigenvalues. This makes it unnecessary to decompose the Hamiltonian into a sum-of-terms like the Trotter-Suzuki methods.

#### Quantum Signal Processing
The quantum signal processing algorithm works by transducing the eigenvalues of the Hamiltonian into an ancilla qubit, transforming the eigenvalues with single qubit rotations and finally projecting the ancilla. It has been proved to be optimal in query complexity when it comes to Hamiltonian simulation.

### Complexity
The table of the complexities of the Hamiltonian simulation algorithms mentioned above. The Hamiltonian simulation can be studied in two ways. This depends on how the Hamiltonian is given. If it is given explicitly, then gate complexity matters more than query complexity. If the Hamiltonian is described as an Oracle black box then the number of queries to the oracle is more important than the gate count of the circuit. The following table shows the gate and query complexity of the previously mentioned techniques.

![[Screenshot 2023-02-23 at 11.13.11 AM.png]]

#QuantumComputing 

Stabiliser circuits, i.e. [[Clifford Circuits]] can be perfectly simulated in polynomial time on a probabilistic classical computer. 

### Formal
Theorem: A quantum circuit using only the following elements can be simulated efficiently on a classical computer:
1. Preparation of qubits in computational basis states
2. Clifford gates (Hadamard gates, controlled NOT gates, phase gate $S$)
3. Measurements in the computational basis.

The Gottesman-Knill theorem shows that even some highly entangled states can be simulated efficiently. Several important types of quantum algorithms use only Clifford gates, most importantly the standard algorithms for entanglement distillation and for quantum error correction. From a practical point of view, stabiliser circuits have been simulated in $0(n \log n)$ time using the graph state formalism.

### Stabiliser Group of $\ket{\psi}$
$U$ stabilises $\ket{\psi}$ if $U\ket{\psi} =\ket{\psi}$ 
For any state $\ket{\psi}$,  $\{U: U\ket{\psi} = \ket{\psi}\}$ is a set of unitaries which forms a group.


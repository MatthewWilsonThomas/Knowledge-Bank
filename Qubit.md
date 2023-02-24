#QuantumComputing 
#QuantumMechanics

### Single Qubits
A Quantum Bit (Qubit) is the fundamental unity of quantum computing. The quantum qubit is a linear combination of any quantum states (with specific amplitudes)
$$
|\psi\rangle=\alpha|0\rangle+\beta|1\rangle
$$
i.e. a superposition of quantum states. 
This quantum bit will be measured at state $\ket{0}$ with $P[\ket{0}]=\alpha^2$ and $P[\ket{1}]=\beta^2$. Since these are probabilities we can write (they sum to 1):
$$
|\psi\rangle=e^{i \gamma}\left(\cos \frac{\theta}{2}|0\rangle+e^{i \varphi} \sin \frac{\theta}{2}|1\rangle\right)
$$
Further, since the global phase has no effect on measurement (i.e. is not observable) we can simplify to:
$$
|\psi\rangle=\cos \frac{\theta}{2}|0\rangle+e^{i \varphi} \sin \frac{\theta}{2}|1\rangle
$$
This shows how we can visually represent qubits as locations on a Bloch Sphere:![[Screenshot 2023-02-15 at 9.34.12 AM.png]]
### Multiple Qubits
We can also have multiple quantum states, i.e. for two states we get:
$$
|\psi\rangle=\alpha_{00}|00\rangle+\alpha_{01}|01\rangle+\alpha_{10}|10\rangle+\alpha_{11}|11\rangle
$$
In this state we can measure either the first, second, or both qubit. If we measure the first qubit then we have to update the amplitudes of the second state using a form of [[Bayesian Updating]]. The post-measurement state becomes:
$$
\left|\psi^{\prime}\right\rangle=\frac{\alpha_{00}|00\rangle+\alpha_{01}|01\rangle}{\sqrt{\left|\alpha_{00}\right|^2+\left|\alpha_{01}\right|^2}}
$$
We can then generalise further to an arbitrary $N$ state quantum qubit:
$$
\ket{\psi} = \frac{1}{\sqrt{2^n}}\sum_{i=0}^{N}\alpha_i\ket{x_i}
$$

### Measurement
The possible measurement outcomes of a quantum state i.e. qubit are the basis vectors, these can also be viewed as the eigenstates of the vectors. 

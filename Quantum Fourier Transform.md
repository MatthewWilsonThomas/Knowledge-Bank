#Algorithm 
#FourierAnalysis 
#DiscreteMathematics 
#QuantumComputing

The QFT is a linear transformation of quantum bits, it is the Quantum analogue to the [[Discrete Fourier Transform]]. It is used in [[Shor's]] and the [[Quantum Phase Estimation]] Algorithm. 

### Definition
The QFT is the [[Discrete Fourier Transform]] applied to the vector of amplitudes of a quantum state, which is a vector of length $N=2^n$. 
The classical fourier transform acts according to:
$$
y_k=\frac{1}{\sqrt{N}} \sum_{n=0}^{N-1} x_n \omega_N^{-k n}, \quad k=0,1,2, \ldots, N-1
$$
with $\omega_N=e^{\frac{2 \pi i}{N}}$ and $\omega_N^n$ is an N-th root of unity. 

The QFT acts on a state $\ket{x}=\sum_{i=1}^{N-1}x_i\ket{i}$ and maps it to a quantum state $\sum_{i=1}^{N-1} y_x\ket{i}$ with: 
$$
y_k=\frac{1}{\sqrt{N}} \sum_{n=0}^{N-1} x_n \omega_N^{n k}, \quad k=0,1,2, \ldots, N-1
$$
Since $\omega_N^n$ is a rotation, the inverse QFT acts similary but with:
$$
x_n=\frac{1}{\sqrt{N}} \sum_{k=0}^{N-1} y_k \omega_N^{-n k}, \quad k=0,1,2, \ldots, N-1
$$

We can also view the QFT as a [[Unitary Matrix]] acting on quantum state vectors, i.e.:
![[Screenshot 2023-02-15 at 9.12.23 AM.png]]

### Circuit Implementation
The [[Quantum Gate]] used in the circuit of $n$ qubits, are the Hadamard Gate and the Phase Gate $R_n$
$$
H=\frac{1}{\sqrt{2}}\left(\begin{array}{cc}
1 & 1 \\
1 & -1
\end{array}\right) \quad \text { and } \quad R_n=\left(\begin{array}{cc}
1 & 0 \\
0 & e^{2 \pi i / N}
\end{array}\right)
$$
The circuit is then composed as:
![[Screenshot 2023-02-15 at 9.14.46 AM.png]]


### Compact Expression
The QFT can be expressed in a compact manner as the tensor product of a series of terms:
$$
\operatorname{QFT}\left(\left|x_1 x_2 \ldots x_n\right\rangle\right)=\frac{1}{\sqrt{N}}\left(|0\rangle+e^{2 \pi i\left[0 . x_n\right]}|1\rangle\right) \otimes\left(|0\rangle+e^{2 \pi i\left[0 . x_{n-1} x_n\right]}|1\rangle\right) \otimes \cdots \otimes\left(|0\rangle+e^{2 \pi i\left[0 . x_1 x_2 \ldots x_n\right]}|1\rangle\right)
$$


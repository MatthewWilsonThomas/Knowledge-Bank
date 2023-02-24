#QuantumComputing 
#Algorithm 

An algorithm for efficiently counting the number of solutions for a given search problem, based on the [[Quantum Phase Estimation]] and [[Grover's Search]] Algorithms. 

### Problem 
Consider a finite set $\{0,1\}^n$ of size $N=2^n$ and a set $B$ of "solutions" (that is a subset of $\{0,1\}^n$ ). Define:
$$
\left\{\begin{array}{l}
f:\{0,1\}^n \rightarrow\{0,1\} \\
f(x)= \begin{cases}1 & x \in B \\
0 & x \notin B\end{cases}
\end{array}\right.
$$
In other words, $f$ is the indicator function of $B$.
Calculate the number of solutions $M=\left|f^{-1}(1)\right|=|B|$

### Algorithm
![[Screenshot 2023-02-23 at 11.06.48 AM.png]]

#### Setup
Input consists of two registers, upper $p$ qubits as the first register and the lower $n$ qubits as the second register.

#### Create Superposition
The initial state of the system is $|0\rangle^{\otimes p}|0\rangle^{\otimes n}$. After applying multiple bit Hadamard gate operation on each of the registers separately, the state of the first register is
$$
\frac{1}{2^{p / 2}}(|0\rangle+|1\rangle)^{\otimes p}
$$
and the state of the second register is
$$
\frac{1}{2^{n / 2}}(|0\rangle+|1\rangle)^{\otimes n}=\frac{1}{\sqrt{N}} \sum_{x=0}^{N-1}|x\rangle
$$
an equal superposition state in the computational basis.

#### Apply the Grover Operator
Because the size of the space is $\left|\{0,1\}^n\right|=2^n=N$ and the number of solutions is $|B|=M$, we can define the normalised states:
$$
|\alpha\rangle=\frac{1}{\sqrt{N-M}} \sum_{x \notin B}|x\rangle, \quad \text { and } \quad|\beta\rangle=\frac{1}{\sqrt{M}} \sum_{x \in B}|x\rangle
$$
Note that
$$
\sqrt{\frac{N-M}{N}}|\alpha\rangle+\sqrt{\frac{M}{N}}|\beta\rangle=\frac{1}{\sqrt{N}} \sum_{x=0}^{N-1}|x\rangle
$$
which is the state of the second register after the Hadamard transform.
Geometric visualisation of Grover's algorithm shows that in the two-dimensional space spanned by $|\alpha\rangle$ and $|\beta\rangle$, the Grover operator is a counterclockwise rotation; hence, it can be expressed as
$$
G=\left[\begin{array}{cc}
\cos \theta & -\sin \theta \\
\sin \theta & \cos \theta
\end{array}\right]
$$
in the orthonormal basis $\{|\alpha\rangle,|\beta\rangle\}$ 
From the properties of rotation matrices we know that $G$ is a unitary matrix with the two eigenvalues $e^{\pm i \theta}$.

#### Estimate the Value of $\theta$
From here onwards, we follow the quantum phase estimation algorithm scheme: we apply controlled Grover operations followed b inverse quantum Fourier transform; and according to the analysis, we will find the best $p$-bit approximation to the real number $\theta$ (belonging to the eigenvalues $e^{\pm i \theta}$ of the Grover operator) with probability higher than $\frac{4}{\pi^2}$

Note that the second register is actually in a superposition of the eigenvectors of the Grover operator (while in the original quantum phase estimation algorithm, the second register is the required eigenvector). This means that with some probability, we approximate $\theta$, and with some probability, we approximate $2 \pi-\theta$; those two approximations are equivalent.

### Analysis
Assuming that the size $N$ of the space is at least twice the number of solutions (namely, assuming that $M \leq \frac{N}{2}$ ), a result of the analysis of Grover's algorithm is:
$$
\sin \frac{\theta}{2}=\sqrt{\frac{M}{N}} .
$$
Thus, if we find $\theta$, we can also find the value of $M$ (because $N$ is known).
The error
$$
\frac{|\Delta M|}{N}=\left|\sin ^2\left(\frac{\theta+\Delta \theta}{2}\right)-\sin ^2\left(\frac{\theta}{2}\right)\right|
$$
is determined by the error within estimation of the value of $\theta$. The quantum phase estimation algorithm finds, with high probability, the best $p$-bit approximation of $\theta$; this means that if $p$ is large enough, we will have $\Delta \theta \approx 0$, hence $|\Delta M| \approx 0$
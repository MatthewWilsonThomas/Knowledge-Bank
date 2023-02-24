#Algorithm 
#QuantumComputing 

### Problem Statement
Let $U$ be a Unitary operator (i.e. [[Unitary Matrix]]) that operates on $m$ qubit with an eigenvector $\ket{\psi}$ , such that $U\ket{\psi} = e^{2\pi i \theta}\ket{\psi}, 0 \leq \theta\leq 1$. We would like to find the eigenvalue $e^{2\pi i \theta}$ of $\ket{\psi}$, i.e. estimate the phase $\theta$, to a finite level of precision. We can write the eigenvalue in the form $e^{2\pi i \theta}$ because $U$ is a unitary operator over a complex vector space, so its eigenvalues must be complex numbers with the absolute value $1$. 

### Algorithm
![[Screenshot 2023-02-19 at 12.03.30 PM.png]]
#### Initialization
The intial state og the system is $\ket{0}^{\otimes n}\ket{\psi}$.

#### Create Superposition
We apply the $n$-bit Hadamard Transform on the first register giving the new state as $$\frac{1}{\sqrt{2^N}} (\ket{0} +\ket{1})^{\otimes n} \ket{\psi}$$
#### Apply Controlled Unitary Operations
Let $U$ be a unitary operator with eigenvector $|\psi\rangle$ such that $U|\psi\rangle=e^{2 \pi i \theta}|\psi\rangle$; thus by exponentiation by squaring,
$$
U^{2^j}|\psi\rangle=U^{2^{j-1}} U^{2^{j-1}}|\psi\rangle=U^{2^{j-1}} e^{2 \pi i 2^{j-1} \theta}|\psi\rangle=e^{2 \pi i 2^j \theta}|\psi\rangle
$$
$C-U$ is a controlled- $U$ gate which applies the unitary operator $U$ on the second register only if its corresponding control bit (from the first register) is $|1\rangle$.

Assuming for the sake of clarity that the controlled gates are applied sequentially, after applying $C-U^{2^0}$ to the $n^{\text {th }}$ qubit of the first register and the second register, the state becomes
$$
\begin{aligned}
& \frac{1}{2^{\frac{1}{2}}} \underbrace{\left(|0\rangle|\psi\rangle+|1\rangle e^{2 \pi i 2^0 \theta}|\psi\rangle\right)}_{n^{\text {th }} \text { qubit and second register }} \otimes \frac{1}{2^{\frac{n-1}{2}}} \underbrace{(|0\rangle+|1\rangle)^{\otimes^{n-1}}}_{\text {qubits } 1^{\text {st }} \text { to } n-1^{\text {th }}}=\frac{1}{2^{\frac{1}{2}}}\left(|0\rangle|\psi\rangle+e^{2 \pi i 2^0 \theta}|1\rangle|\psi\rangle\right) \otimes \frac{1}{2^{\frac{n-1}{2}}}(|0\rangle+|1\rangle)^{\otimes^{n-1}} \\
& =\frac{1}{2^{\frac{1}{2}}}\left(|0\rangle+e^{2 \pi i 2^0 \theta}|1\rangle\right)|\psi\rangle \otimes \frac{1}{2^{\frac{n-1}{2}}}(|0\rangle+|1\rangle)^{\otimes^{n-1}}=\frac{1}{2^{\frac{n}{2}}} \underbrace{\left(|0\rangle+e^{2 \pi i 2^0 \theta}|1\rangle\right)}_{n^{\text {th }} \text { qubit }} \otimes(|0\rangle+|1\rangle)^{\otimes^{n-1}}|\psi\rangle,
\end{aligned}
$$
where we use:
$$
|0\rangle|\psi\rangle+|1\rangle \otimes e^{2 \pi i 2^j \theta}|\psi\rangle=\left(|0\rangle+e^{2 \pi i 2^j \theta}|1\rangle\right)|\psi\rangle, \forall j
$$
After applying all the remaining $n-1$ controlled operations $C-U^{2^j}$ with $1 \leq j \leq n-1$, as seen in the figure, the state of the first register can be described as
$$
\frac{1}{2^{\frac{n}{2}}} \underbrace{\left(|0\rangle+e^{2 \pi i 2^{n-1} \theta}|1\rangle\right)}_{1^{\text {st }} \text { qubit }} \otimes \cdots \otimes \underbrace{\left(|0\rangle+e^{2 \pi i 2^1 \theta}|1\rangle\right)}_{n-1^{\text {th }} \text { qubit }} \otimes \underbrace{\left(|0\rangle+e^{2 \pi i 2^0 \theta}|1\rangle\right)}_{n^{\text {th }} \text { qubit }}=\frac{1}{2^{\frac{n}{2}}} \sum_{k=0}^{2^n-1} e^{2 \pi i \theta k}|k\rangle,
$$
where $|k\rangle$ denotes the binary representation of $k$, i.e. it's the $k^{\text {th }}$ computational basis, and the state of the second register is left physically unchanged at $|\psi\rangle$.

#### Apply the Inverse [[Quantum Fourier Transform]]
Applying inverse quantum Fourier transform on
$$
\frac{1}{2^{\frac{n}{2}}} \sum_{k=0}^{2^n-1} e^{2 \pi i \theta k}|k\rangle
$$
yields
$$
\frac{1}{2^{\frac{n}{2}}} \sum_{k=0}^{2^n-1} e^{2 \pi i \theta k} \frac{1}{2^{\frac{n}{2}}} \sum_{x=0}^{2^n-1} e^{\frac{-2 \pi i k x}{2^n}}|x\rangle=\frac{1}{2^n} \sum_{x=0}^{2^n-1} \sum_{k=0}^{2^n-1} e^{2 \pi i \theta k} e^{\frac{-2 \pi i k x}{2^n}}|x\rangle=\frac{1}{2^n} \sum_{x=0}^{2^n-1} \sum_{k=0}^{2^n-1} e^{-\frac{2 \pi i k}{2^n}\left(x-2^n \theta\right)}|x\rangle
$$
The state of both registers together is
$$
\frac{1}{2^n} \sum_{x=0}^{2^n-1} \sum_{k=0}^{2^n-1} e^{-\frac{2 \pi i k}{2^n}\left(x-2^n \theta\right)}|x\rangle \otimes|\psi\rangle
$$

#### Phase Approximation Representation
We can approximate the value of $\theta \in[0,1]$ by rounding $2^n \theta$ to the nearest integer. This means that $2^n \theta=a+2^n \delta$, where $a$ is the nearest integer to $2^n \theta$, and the difference $2^n \delta$ satisfies $0 \leqslant\left|2^n \delta\right| \leqslant \frac{1}{2}$.
We can now write the state of the first and second register in the following way:
$$
\frac{1}{2^n} \sum_{x=0}^{2^n-1} \sum_{k=0}^{2^n-1} e^{-\frac{2 \pi i k}{2^n}(x-a)} e^{2 \pi i \delta k}|x\rangle \otimes|\psi\rangle
$$
#### Measurement
Performing a measurement in the computational basis on the first register yields the result $|a\rangle$ with probability
$$
\operatorname{Pr}(a)=\left|\underbrace{\left\langle\left|\frac{1}{2^n} \sum_{x=0}^{2^n-1} \sum_{k=0}^{2^n-1} e^{\frac{-2 \pi i k}{2^n}(x-a)} e^{2 \pi i \delta k}\right| x\right\rangle}_{\text {State of the first register }}\right|^2=\frac{1}{2^{2 n}}\left|\sum_{k=0}^{2^n-1} e^{2 \pi i \delta k}\right|^2= \begin{cases}1 & \delta=0 \\ \frac{1}{2^{2 n}}\left|\frac{1-e^{2 \pi i 2^n \delta}}{1-e^{2 \pi i \delta}}\right|^2 & \delta \neq 0\end{cases}
$$
For $\delta=0$ the approximation is precise, thus $a=2^n \theta$ and $\operatorname{Pr}(a)=1$. In this case, we always measure the accurate value of the phase. ${ }^{[3]: 157[4]: 347}$ The state of the system after the measurement is $\left|2^n \theta\right\rangle \otimes|\psi\rangle{ }^{[2]: 223}$

For $\delta \neq 0$ since $|\delta| \leqslant \frac{1}{2^{n+1}}$ the algorithm yields the correct result with probability $\operatorname{Pr}(a) \geqslant \frac{4}{\pi^2} \approx 0.405$. We prove this as follows: ${ }^{[3]: 157[4]: 348}$
$$
\begin{aligned}
\operatorname{Pr}(a) & =\frac{1}{2^{2 n}}\left|\frac{1-e^{2 \pi i 2^n \delta}}{1-e^{2 \pi i \delta}}\right|^2 \quad & \text { for } \delta \neq 0 \\
& =\frac{1}{2^{2 n}}\left|\frac{2 \sin \left(\pi 2^n \delta\right)}{2 \sin (\pi \delta)}\right|^2 \quad & \left|1-e^{2 i x}\right|^2=4|\sin (x)|^2 \\
& =\frac{1}{2^{2 n}} \frac{\left|\sin \left(\pi 2^n \delta\right)\right|^2}{|\sin (\pi \delta)|^2} & \\
& \geqslant \frac{1}{2^{2 n}} \frac{\left|\sin \left(\pi 2^n \delta\right)\right|^2}{|\pi \delta|^2} & |\sin (\pi \delta)| \leqslant|\pi \delta| \text { for }|\delta| \leqslant \frac{1}{2^{n+1}} \\
& \geqslant \frac{1}{2^{2 n}} \frac{\left|2 \cdot 2^n \delta\right|^2}{|\pi \delta|^2} & \left|2 \cdot 2^n \delta\right| \leqslant\left|\sin \left(\pi 2^n \delta\right)\right| \text { for }|\delta| \leqslant \frac{1}{2^{n+1}} \\
& \geqslant \frac{4}{\pi^2} &
\end{aligned}
$$
This result shows that we will measure the best $n$-bit estimate of $\theta$ with high probability. By increasing the number of qubits by $O(\log (1 / \epsilon))$ and ignoring those last qubits we can increase the probability to $1-\epsilon$.

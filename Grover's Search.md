#Algorithm 
#QuantumComputing 
#Search

Grover's Algorithm is the quantum search algorithm. It finds (with high probability) the input to a black box which produces the specified output. 

### Problem Statement
Suppose we have a function $f: \{0, 1, ..., N-1 \}\rightarrow \{0, 1\}$.  We additionaly assume that only one index $f(x) = 1$, this index is $\omega$. The goal is to identity $\omega$. 

We access $f$ with a Unitary Oracle $U_\omega$:
$$
\begin{cases} 
	U_\omega\ket{x} = -\ket{x} \forall x = \omega, i.e. f(x) = 1\\
	U_\omega\ket{x} = \ket{x} \forall x \neq \omega, i.e. f(x) = 0
\end{cases}
$$
This uses the $N$ dimensional state-space $\mathcal{H}$ which is supplied by a register of $n = \log_2N$ qubits:
$$
U_\omega \ket{x} = (-1)^{f(x)}\ket{x}
$$

The algorithm outputs $\omega$ with a probability at least $1/2$ using $O(\sqrt{N})$ applications of $U_\omega$. To increase this probability we can run Grover's multiple times. 

### Algorithm
![[Screenshot 2023-02-19 at 11.45.55 AM.png]]
1. Initialize the system to the uniform superposition over all states: $$\ket{s} = \frac{1}{\sqrt{N}} \sum_{x=0}^{N-1}\ket{x}$$
2. Perform the following Grover Iteration $r(N)$ times: 
	1. Apply the $U_\omega$ operator.
	2. Apply the Grover Diffusion Operator $U_S = 2\ket{s}\bra{s} - I$.
3. Measure the resulting Quantum State in the computational basis.
For the correctly chosen value of $r$, the output will be $\ket{\omega}$ with probability approaching $1$ for $N>>1$. Analysis shows that this eventual value for $r(N)$ satisfies $r(N)\leq \lceil\frac{\pi}{4}\sqrt{N}\rceil$.

### Multiple Matching Entries
If, instead of 1 matching entry, there are $k$ matching entries, the same algorithm works, but the number of iterations must be $\frac{\pi}{4}\left(\frac{N}{k}\right)^{1 / 2}$ instead of $\frac{\pi}{4} N^{1 / 2}$.
There are several ways to handle the case if $k$ is unknown. A simple solution performs optimally up to a constant factor: run Grover's algorithm repeatedly for increasingly small values of $k$, e.g., taking $k=N, N / 2, N / 4, \ldots$, and so on, taking $k=N / 2^t$ for iteration $t$ until a matching entry is found.
With sufficiently high probability, a marked entry will be found by iteration $t=\log _2(N / k)+c$ for some constant $c$. Thus, the total number of iterations taken is at most
$$
\frac{\pi}{4}\left(1+\sqrt{2}+\sqrt{4}+\cdots+\sqrt{\frac{N}{k 2^c}}\right)=O(\sqrt{N / k})
$$

### Proofs of Correctness 
#### Geometric Proof
There is a geometric interpretation of Grover's algorithm, following from the observation that the quantum state of Grover's algorithm stays in a two-dimensional subspace after each step. Consider the plane spanned by $|s\rangle$ and $|\omega\rangle$; equivalently, the plane spanned by $|\omega\rangle$ and the perpendicular $\left|s^{\prime}\right\rangle=\frac{1}{\sqrt{N-1}} \sum_{x \neq \omega}|x\rangle$.
Grover's algorithm begins with the initial ket $|s\rangle$, which lies in the subspace. The operator $U_\omega$ is a reflection at the hyperplane orthogonal to $|\omega\rangle$ for vectors in the plane spanned by $\left|s^{\prime}\right\rangle$ and $|\omega\rangle$, i.e. it acts as a $|\omega\rangle$ reflection across $\left|s^{\prime}\right\rangle$. This can be seen by writing $U_\omega$ in the form of a Householder reflection:
$$
U_\omega=I-2|\omega\rangle\langle\omega|
$$
The operator $U_s=2|s\rangle\langle s|-I$ is a reflection through $|s\rangle$. Both  operators $U_s$ and $U_\omega$ take states in the plane spanned by $\left|s^{\prime}\right\rangle$ and $|\omega\rangle$ to states in the plane. Therefore, Grover's algorithm stays in this plane for the entire algorithm.
![[Screenshot 2023-02-21 at 11.31.36 AM.png]]
It is straightforward to check that the operator $U_s U_\omega$ of each Grover iteration step rotates the state vector by an angle of $\theta=2 \arcsin \frac{1}{\sqrt{N}}$. So, with enough iterations, one can rotate from the initial state $|s\rangle$ to the desired output state $|\omega\rangle$. The initial ket is close to the state orthogonal to $|\omega\rangle$:
$\left\langle s^{\prime} \mid s\right\rangle=\sqrt{\frac{N-1}{N}}$
In geometric terms, the angle $\theta / 2$ between $|s\rangle$ and $\left|s^{\prime}\right\rangle$ is given by
$$
\sin \frac{\theta}{2}=\frac{1}{\sqrt{N}}
$$
We need to stop when the state vector passes close to $|\omega\rangle$; after this, subsequent iterations rotate the state vector away from $|\omega\rangle$, reducing the probability of obtaining the correct answer. The exact probability of measuring the correct answer is
$$
\sin ^2\left(\left(r+\frac{1}{2}\right) \theta\right)
$$
where $r$ is the (integer) number of Grover iterations. The earliest time that we get a near-optimal measurement is therefore $r \approx \pi \sqrt{N} / 4$.

#### Algebraic Proof
To complete the algebraic analysis, we need to find out what happens when we repeatedly apply $U_s U_\omega$. A natural way to do this is by eigenvalue analysis of a matrix. Notice that during the entire computation, the state of the algorithm is a linear combination of $s$ and $\omega$. We can write the action of $U_s$ and $U_\omega$ in the space spanned by $\{|s\rangle,|\omega\rangle\}$ as:
$$
\begin{aligned}
& U_s: a|\omega\rangle+b|s\rangle \mapsto[|\omega\rangle|s\rangle]\left[\begin{array}{cc}
-1 & 0 \\
2 / \sqrt{N} & 1
\end{array}\right]\left[\begin{array}{l}
a \\
b
\end{array}\right] . \\
& U_\omega: a|\omega\rangle+b|s\rangle \mapsto[|\omega\rangle|s\rangle]\left[\begin{array}{cc}
-1 & -2 / \sqrt{N} \\
0 & 1
\end{array}\right]\left[\begin{array}{l}
a \\
b
\end{array}\right] .
\end{aligned}
$$
So in the basis $\{|\omega\rangle,|s\rangle\}$ (which is neither orthogonal nor a basis of the whole space) the action $U_s U_\omega$ of applying $U_\omega$ followed by $U_s$ is given by the matrix
$$
U_s U_\omega=\left[\begin{array}{cc}
-1 & 0 \\
2 / \sqrt{N} & 1
\end{array}\right]\left[\begin{array}{cc}
-1 & -2 / \sqrt{N} \\
0 & 1
\end{array}\right]=\left[\begin{array}{cc}
1 & 2 / \sqrt{N} \\
-2 / \sqrt{N} & 1-4 / N
\end{array}\right]
$$
This matrix happens to have a very convenient Jordan form. If we define $t=\arcsin (1 / \sqrt{N})$, it is
$$
U_s U_\omega=M\left[\begin{array}{cc}
e^{2 i t} & 0 \\
0 & e^{-2 i t}
\end{array}\right] M^{-1} \text { where } M=\left[\begin{array}{cc}
-i & i \\
e^{i t} & e^{-i t}
\end{array}\right]
$$
It follows that $r$-th power of the matrix (corresponding to $r$ iterations) is
$$
\left(U_s U_\omega\right)^r=M\left[\begin{array}{cc}
e^{2 r i t} & 0 \\
0 & e^{-2 r i t}
\end{array}\right] M^{-1} .
$$
Using this form, we can use trigonometric identities to compute the probability of observing $\omega$ after $r$ iterations mentioned in the previous section,
Alternatively, one might reasonably imagine that a near-optimal time to distinguish would be when the angles $2 r t$ and $-2 r t$ are as far apart as possible, which corresponds to $2 r t \approx \pi / 2$, or $r=\pi / 4 t=\pi / 4 \arcsin (1 / \sqrt{N}) \approx \pi \sqrt{N} / 4$. Then the system is in state
$$
[|\omega\rangle|s\rangle]\left(U_s U_\omega\right)^r\left[\begin{array}{l}
0 \\
1
\end{array}\right] \approx[|\omega\rangle|s\rangle] M\left[\begin{array}{cc}
i & 0 \\
0 & -i
\end{array}\right] M^{-1}\left[\begin{array}{l}
0 \\
1
\end{array}\right]=|\omega\rangle \frac{1}{\cos (t)}-|s\rangle \frac{\sin (t)}{\cos (t)}
$$
A short calculation now shows that the observation yields the correct answer $\omega$ with error $O\left(\frac{1}{N}\right)$.

### Applications
Grover's Algorithm can be used to speed up a braod range of algorithms, in particular, NP-complete problems with an exhaustive search algorithm. In these cases Grover's in a quadratic speedup over the [[3SAT]] algortihm
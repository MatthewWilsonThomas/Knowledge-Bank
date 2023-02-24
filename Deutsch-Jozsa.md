#Algorithm 
#QuantumComputing 

### Problem Statement
In the Deutsch-Jozsa problem, we are given a black box quantum computer known as an oracle that implements some function:
$$
f:\{0,1\}^n \rightarrow\{0,1\}
$$
The function takes $n$-bit binary values as input and produces either a 0 or a 1 as output for each such value. We are promised that the function is either constant ( 0 on all inputs or 1 on all inputs) or balanced ( 1 for exactly half of the input domain and 0 for the other half). The task then is to determine if $f$ is constant or balanced by using the oracle.

### Classical Solution
For a conventional deterministic algorithm where $n$ is the number of bits, $2^{n-1}+1$ evaluations of $f$ will be required in the worst case. To prove that $f$ is constant, just over half the set of inputs must be evaluated and their outputs found to be identical (because the function is guaranteed to be either balanced or constant, not somewhere in between). The best case occurs where the function is balanced and the first two output values are different. For a conventional randomized algorithm, a constant $k$ evaluations of the function suffices to produce the correct answer with a high probability (failing with probability $\epsilon ≥1$ with $k\geq 1$. However, $k=2^{n-1}+1$ evaluations are still required if we want an answer that has no possibility of error. The Deutsch-Jozsa quantum algorithm produces an answer that is always correct with a single evaluation of $f$.

### Circuit Implementation
![[Screenshot 2023-02-15 at 10.10.03 AM.png]]
### Quantum Algorithm
The algorithm begins in state:
$$ \ket{\psi_0} = \ket{0}^{\otimes n} \ket{1} $$
Applies a Hadamard Transform to each state to get:
$$
\ket{\psi_1} = \frac{1}{\sqrt{2^{n+1}}} \sum_{x=0}^{2^n-1}|x\rangle(|0 \oplus f(x)\rangle-|1 \oplus f(x)\rangle)
$$
Apply the Quantum Oracle to get:
$$
\ket{\psi_2} = \frac{1}{\sqrt{2^{n+1}}} \sum_{x=0}^{2^n-1}|x\rangle(|0 \oplus f(x)\rangle-|1 \oplus f(x)\rangle)
$$
By considering the two cases of $f(x) \in \{0, 1\}$ we can see this is equal to:
$$
\ket{\psi_2} = \frac{1}{\sqrt{2^{n+1}}} \sum_{x=0}^{2^n-1}(-1)^{f(x)}|x\rangle(|0\rangle-|1\rangle)
$$
We can also ignore the final qubit:
$$
\ket{\psi_2} = \frac{1}{\sqrt{2^{n+1}}} \sum_{x=0}^{2^n-1}(-1)^{f(x)}|x\rangle
$$
Then we apply the Hadamard Transform:
$$
H^{\otimes n}|k\rangle=\frac{1}{\sqrt{2^n}} \sum_{j=0}^{2^n-1}(-1)^{k \cdot j}|j\rangle
$$
To get:
$$
\ket{\psi_3} = \frac{1}{\sqrt{2^n}} \sum_{x=0}^{2^n-1}(-1)^{f(x)}\left[\frac{1}{\sqrt{2^n}} \sum_{y=0}^{2^n-1}(-1)^{x \cdot y}|y\rangle\right]=\sum_{y=0}^{2^n-1}\left[\frac{1}{2^n} \sum_{x=0}^{2^n-1}(-1)^{f(x)}(-1)^{x \cdot y}\right]|y\rangle
$$
### Measurement
We can see from measuring $\ket{\psi_3}$ that the probability of state $k$ appearing is:
$$
\left|\frac{1}{2^n} \sum_{x=0}^{2^n-1}(-1)^{f(x)}(-1)^{x \cdot k}\right|^2
$$
So the probability of measuring $k=0$ is:
$$
\left|\frac{1}{2^n} \sum_{x=0}^{2^n-1}(-1)^{f(x)}\right|^2
$$
This evaluates to 1 if $f(x)$ is constant (constructive interference) and 0 if $f(x)$ is balanced (destructive inteference), i.e. the final measurement will always answer the question with certainty. 
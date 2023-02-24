#Algorithm 
#QuantumComputing 

### Problem Statement
Given an oracle that implements a function $f:\{0,1\}^n \rightarrow\{0,1\}$ in which $f(x)$ is promised to be the dot product between $x$ and a secret string $s \in\{0,1\}^n$ modulo 2, $f(x)=x \cdot s=x_1 s_1 \oplus x_2 s_2 \oplus \cdots \oplus x_n s_n$, find $s$.

### Classical Solution
Classically, the most efficient method to find the secret string is by evaluating the function $n$ times with the input values $x=2^i$ for all
$$
\begin{aligned}
& i \in\{0,1, \ldots, n-1\}: \\
& f\left(1000 \cdots 0_n\right)=s_1 \\
& f\left(0100 \cdots 0_n\right)=s_2 \\
& f\left(0010 \cdots 0_n\right)=s_3 \\
& ... \\
& f\left(0000 \cdots 1_n\right)=s_n
\end{aligned}
$$
In contrast to the classical solution which needs at least $n$ queries of the function to find $s$, only one query is needed using quantum computing.

### Circuit Implementation
![[Screenshot 2023-02-15 at 10.11.27 AM.png]]

### Algorithm
We start in the $n$-qubit state:
$$
\ket{\psi_0} = \ket{0}^{\otimes n}
$$
We then apply the Hadamard Gate:
$$
\ket{\psi_1} = \frac{1}{\sqrt{2^n}} \sum_{x=0}^{2^n-1}|x|
$$
Then applying the Oracle $U_f:\ket{x}\rightarrow(-1)^{f(x)}\ket{x}$. Transforming the state to:
$$
\ket{\psi_3} = \frac{1}{\sqrt{2^n}} \sum_{x=0}^{2^n-1}(-1)^{f(x)}|x\rangle
$$
This Oracle is simulated by applying the Standard Orcale $S_f:\ket{b}\ket{x}\rightarrow\ket{b\otimes f(x)}\ket{x}$ by applying this Oracle to $\frac{\ket{0}-\ket{1}}{\sqrt{2}}\ket{x}$. 

Then we Hadamard this state again, so that is $s_i=1$ the state is converted from $\ket{-} \rightarrow \ket{1}$ and if $s_i=0$ the state is converted from $\ket{+}\rightarrow\ket{0}$. We then obtain $s$ by measuring in the standard basis. 

Overall the algorithm performs the following:
$$
|0\rangle^n \stackrel{H^{\otimes n}}{\longrightarrow} \frac{1}{\sqrt{2^n}} \sum_{x \in\{0,1\}^n}|x\rangle \stackrel{U_f}{\longrightarrow} \frac{1}{\sqrt{2^n}} \sum_{x \in\{0,1\}^n}(-1)^{f(x)}|x\rangle \stackrel{H^{\otimes n}}{\longrightarrow} \frac{1}{2^n} \sum_{x, y \in\{0,1\}^n}(-1)^{f(x)+x \cdot y}|y\rangle=|s\rangle
$$
This last stage holds true since for a particular $y$ we have:
$$
\frac{1}{2^n} \sum_{x \in\{0,1\}^n}(-1)^{f(x)+x \cdot y}=\frac{1}{2^n} \sum_{x \in\{0,1\}^n}(-1)^{x \cdot s+x \cdot y}=\frac{1}{2^n} \sum_{x \in\{0,1\}^n}(-1)^{x \cdot(s \oplus y)}=1 \text { if } s \oplus y=\overrightarrow{0}, 0 \text { otherwise}
$$

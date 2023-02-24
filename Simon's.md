#Algorithm 
#QuantumComputing 

The algorithm for solving Simon's Problem served as the inspiration for [[Shor's]]

### Problem
Given a function (implemented by a black box or oracle) $f:\{0,1\}^n \rightarrow\{0,1\}^n$ with the promise that, for some unknown $s \in\{0,1\}^n$, for all $x, y \in\{0,1\}^n$,  $f(x)=f(y)$ if and only if $x \oplus y \in\left\{0^n, s\right\}$ where $\oplus$ denotes bitwise XOR. The goal is to identify $s$ by making as few queries to $f(x)$ as possible. 
Note that $a \oplus b=0^n$ if and only if $a=b$.

Furthermore, for some $x$ and $s$ in $x \oplus y=s, y$ is unique (not equal to $x$ ) if and only if $s \neq 0^n$. This means that $f$ is two-to-one when $s \neq 0^n$, and one-to-one when $s=0^n$. It is also the case that $x \oplus y=s$ implies $y=s \oplus x$, meaning that
$$
f(x)=f(y)=f(x \oplus s)
$$
which shows how $f$ is periodic.

### Classical Algorithm
1. Run the Quantum Subroutine an expected $O(n)$ times to get a list of linearly independent bitstrings $y_1, y_2, ..., y_{n-1}$.
2. Each $y_k$ satisfies $y_k\cdot s = 0$, so we can solve the system of equations this produces to get $s$. 

### Quantum Subroutine
![[Screenshot 2023-02-17 at 12.14.44 PM.png]]
The quantum circuit is the implementation of the quantum part of Simon's algorithm. It makes heavy use of the Hadamard Transform. 

1. Starting state $\ket{0}^{\otimes n}\ket{0}^{\otimes n}$
2. Apply the Hadamard to the first register: $$
\frac{1}{\sqrt{2^n}} \sum_{k=0}^{2^n-1}|k\rangle|0\rangle^{\otimes n}
$$
3. Query the Oracle $U_f$ to get the state: $$
\frac{1}{\sqrt{2^n}} \sum_{k=0}^{2^n-1}|k\rangle|f(k)\rangle
$$
4. Apply another Hadamard Transform to the first register:$$
\frac{1}{\sqrt{2^n}} \sum_{k=0}^{2^n-1}\left[\frac{1}{\sqrt{2^n}} \sum_{j=0}^{2^n-1}(-1)^{j \cdot k}|j\rangle\right]|f(k)\rangle=\sum_{j=0}^{2^n-1}|j\rangle\left[\frac{1}{2^n} \sum_{k=0}^{2^n-1}(-1)^{j \cdot k}|f(k)\rangle\right]
$$
5. Measure the first register, getting the probability of measuring the state $\ket{j}$ as:$$
\| \frac{1}{2^n} \sum_{k=0}^{2^n-1}(-1)^{j \cdot k}|f(k)\rangle \|^2
	$$
There are two cases for our measurement:
1. $s=0^n$ and $f$ is one-to-one.
2. $s \neq 0^n$ and $f$ is two-to-one.
For the first case, since
$$
\| \frac{1}{2^n} \sum_{k=0}^{2^n-1}(-1)^{j \cdot k}|f(k)\rangle \|^2=\frac{1}{2^n}
$$
since in this case, $f$ is one-to-one, implying that the range of $f$ is $\{0,1\}^n$, meaning that the summation is over every basis vector. For the second case, note that there exist two strings, $x_1$ and $x_2$, such that $f\left(x_1\right)=f\left(x_2\right)=z$, where $z \in \operatorname{range}(f)$. We can thus write
$$
\| \frac{1}{2^n} \sum_{k=0}^{2^n-1}(-1)^{j \cdot k}|f(k)\rangle\left\|^2=\right\| \frac{1}{2^n} \sum_{z \in \operatorname{range}(f)}\left((-1)^{j \cdot x_1}+(-1)^{j \cdot x_2}\right)|z\rangle \|^2
$$
Furthermore, since we know that $x_1 \oplus x_2=s$, we know that $x_2=x_1 \oplus s$, and so
$$
\begin{aligned}
\| \frac{1}{2^n} \sum_{z \in \text { range }(f)}\left((-1)^{j \cdot x_1}+(-1)^{j \cdot x_2}\right)|z\rangle \|^2 & =\| \frac{1}{2^n} \sum_{z \in \operatorname{range}(f)}\left((-1)^{j \cdot x_1}+(-1)^{j \cdot\left(x_1 \oplus s\right)}\right)|z\rangle \|^2 \\
& =\| \frac{1}{2^n} \sum_{z \in \operatorname{range}(f)}\left((-1)^{j \cdot x_1}+(-1)^{j \cdot x_1 \oplus j \cdot s}\right)|z\rangle \|^2 \\
& =\| \frac{1}{2^n} \sum_{z \in \operatorname{range}(f)}(-1)^{j \cdot x_1}\left(1+(-1)^{j \cdot s}\right)|z\rangle \|^2
\end{aligned}
$$
This expression is now easy to evaluate. Recall that we are measuring $j$. When $j \cdot s=1$, then this expression will evaluate to 0 , and when $j \cdot s=0$, then this expression will be $2^{-n+1}$.
Thus, both when $s=0^n$ and when $s \neq 0^n$, our measured $j$ satisfies $j \cdot s=0$.


### Complexity
Simon's Algorithm requires $O(n)$ queries to the black box, whereas a classical algorithm would need at least $\Omega(2^{n/2})$ queries. It is also known that Simon's Algorithm is optimal in the sense that any quantum algorithm to solve this problems requires $\Omega(n)$ queries. 
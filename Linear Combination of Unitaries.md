#QuantumComputing 


### Linear Combination of Unitaries
Let $B$ be a linear combination of easy-to-implement unitaries:
$$
B=\sum_i \alpha_i W_i .
$$
Goal: Implement $B$ given the ability to implement select $W=\sum_i|i\rangle\langle i| \otimes W_i$.
For example, let $B=W_0+W_1$.
$$
\begin{aligned}
\text { select } W|+\rangle|\psi\rangle & =\frac{1}{\sqrt{2}}\left(|0\rangle W_0|\psi\rangle+|1\rangle W_1|\psi\rangle\right) \\
& =\frac{1}{2}\left(|+\rangle\left(W_0+W_1\right)|\psi\rangle+|-\rangle\left(W_0-W_1\right)|\psi\rangle\right) \\
& =\frac{1}{2}|+\rangle B|\psi\rangle+\frac{1}{2}|-\rangle\left(W_0-W_1\right)|\psi\rangle
\end{aligned}
$$
This is a probabilistic implementation of $B$.

More generally, we can implement a unitary $V$ that block-encodes $B /\|\alpha\|_1$.
$$
\begin{aligned}
& \text { Define }|A\rangle=\frac{1}{\sqrt{\|\alpha\|_1}} \sum_i \sqrt{\alpha_i}|i\rangle . \\
& \begin{aligned}
\operatorname{select} W|A\rangle|\psi\rangle & =\frac{1}{\sqrt{\|\alpha\|_1}} \sum_i \sqrt{\alpha_i}|i\rangle W_i|\psi\rangle \\
& =\frac{1}{\|\alpha\|_1}|A\rangle B|\psi\rangle+\left|A^{\perp}\right\rangle|\cdots\rangle .
\end{aligned}
\end{aligned}
$$
This is a probabilistic implementation of $B$.

### Application to [[Hamiltonian Simulation]]
Local Hamiltonian simulation problem: Given a local Hamiltonian $H=\sum_j H_j$, implement the unitary $e^{-i H t}$.
- Step 1: Represent $H$ as a linear combination of unitaries. We have $H=\sum_j H_j$, where $H_j$ acts on $O(1)$ qubits. Write $H_j$ in the Pauli basis.
- Step 2: Represent $e^{-i H t}$ as a linear combination of unitaries. Say $H=\sum_i \beta_i P_i$, where $P_i$ are unitary. Then $$
e^{-i H t}=I-i H t+\frac{(i H t)^2}{2 !}+\cdots=I-i t\left(\sum_i \beta_i P_i\right)+\frac{(i t)^2}{2 !}\left(\sum_i \beta_i P_i\right)^2+\cdots
$$ is a linear combination of unitaries!
- Step 3: Apply LCU and OAA. This is the "Truncated [[Taylor Series]]" algorithm "Berry-Childs-Cleve-K-Somma15".

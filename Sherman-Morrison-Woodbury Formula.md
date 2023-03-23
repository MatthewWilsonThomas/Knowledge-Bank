#Mathematics 
#LinearAlgebra 

In mathematics (specifically linear algebra), the Woodbury matrix identity. says that the inverse of a rank-k correction of some matrix can be computed by doing a rank-k correction to the inverse of the original matrix. Alternative names for this formula are the **matrix inversion lemma**, **Sherman–Morrison–Woodbury formula** or just **Woodbury formula**.

### Identity
The Woodbury matrix identity is ${ }^{[5]}$
$$
(A+U C V)^{-1}=A^{-1}-A^{-1} U\left(C^{-1}+V A^{-1} U\right)^{-1} V A^{-1},
$$
where $A, U, C$ and $V$ are conformable matrices: $A$ is $n \times n, C$ is $k \times k, U$ is $n \times k$, and $V$ is $k \times n$. This can be derived using block-wise matrix inversion.

### Proof
The formula can be proven by checking that $(A+U C V)$ times its alleged inverse on the right side of the Woodbury identity gives the identity matrix:
$$
\begin{aligned}
& (A+U C V)\left[A^{-1}-A^{-1} U\left(C^{-1}+V A^{-1} U\right)^{-1} V A^{-1}\right] \\
= & \left\{I-U\left(C^{-1}+V A^{-1} U\right)^{-1} V A^{-1}\right\}+\left\{U C V A^{-1}-U C V A^{-1} U\left(C^{-1}+V A^{-1} U\right)^{-1} V A^{-1}\right\} \\
= & \left\{I+U C V A^{-1}\right\}-\left\{U\left(C^{-1}+V A^{-1} U\right)^{-1} V A^{-1}+U C V A^{-1} U\left(C^{-1}+V A^{-1} U\right)^{-1} V A^{-1}\right\} \\
= & I+U C V A^{-1}-\left(U+U C V A^{-1} U\right)\left(C^{-1}+V A^{-1} U\right)^{-1} V A^{-1} \\
= & I+U C V A^{-1}-U C\left(C^{-1}+V A^{-1} U\right)\left(C^{-1}+V A^{-1} U\right)^{-1} V A^{-1} \\
= & I+U C V A^{-1}-U C V A^{-1} \\
= & I .
\end{aligned}
$$
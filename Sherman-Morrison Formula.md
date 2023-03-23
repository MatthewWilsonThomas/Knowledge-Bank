#Mathematics 
In mathematics, in particular linear algebra, the Sherman–Morrison formula, named after Jack Sherman and Winifred J. Morrison, computes the inverse of the sum of an invertible matrix $\mathcal{A}$ and the outer product $uv^T$ of vectors $u$ and $v$. The Sherman–Morrison formula is a special case of the Woodbury formula.

### Formula 
Suppose $A \in \mathbb{R}^{n \times n}$ is an invertible square matrix and $u, v \in \mathbb{R}^n$ are column vectors. Then $A+u v^{\top}$ is invertible iff $1+v^{\top} A^{-1} u \neq 0$. In this case,
$$
\left(A+u v^{\top}\right)^{-1}=A^{-1}-\frac{A^{-1} u v^{\top} A^{-1}}{1+v^{\top} A^{-1} u}
$$
Here, $u v^{\top}$ is the outer product of two vectors $u$ and $v$.

### Proof
$\Leftrightarrow \Leftarrow$ To prove that the backward direction $1+v^{\top} A^{-1} u \neq 0 \Rightarrow A+u v^{\top}$ is invertible with inverse given as above) is true, we verify the properties of the inverse. A matrix $Y$ (in this case the right-hand side of the Sherman-Morrison formula) is the inverse of a matrix $X$ (in this case $A+u v^{\top}$ ) if and only if $X Y=Y X=I$.
We first verify that the right hand side $(Y)$ satisfies $X Y=I$.
$$
\begin{aligned}
X Y & =\left(A+u v^{\top}\right)\left(A^{-1}-\frac{A^{-1} u v^{\top} A^{-1}}{1+v^{\top} A^{-1} u}\right) \\
& =A A^{-1}+u v^{\top} A^{-1}-\frac{A A^{-1} u v^{\top} A^{-1}+u v^{\top} A^{-1} u v^{\top} A^{-1}}{1+v^{\top} A^{-1} u} \\
& =I+u v^{\top} A^{-1}-\frac{u v^{\top} A^{-1}+u v^{\top} A^{-1} u v^{\top} A^{-1}}{1+v^{\top} A^{-1} u} \\
& =I+u v^{\top} A^{-1}-\frac{u\left(1+v^{\top} A^{-1} u\right) v^{\top} A^{-1}}{1+v^{\top} A^{-1} u} \\
& =I+u v^{\top} A^{-1}-u v^{\top} A^{-1}
\end{aligned}
$$
To end the proof of this direction, we need to show that $Y X=I$ in a similar way as above:
$$
Y X=\left(A^{-1}-\frac{A^{-1} u v^{\top} A^{-1}}{1+v^{\top} A^{-1} u}\right)\left(A+u v^{\top}\right)=I
$$
(In fact, the last step can be avoided since for square matrices $X$ and $Y, X Y=I$ is equivalent to $Y X=I$.)
$\Leftrightarrow$ Reciprocally, if $1+v^{\top} A^{-1} u=0$, then via the matrix determinant lemma, $\operatorname{det}\left(A+u v^{\top}\right)=\left(1+v^{\top} A^{-1} u\right) \operatorname{det}(A)=0$, so $\left(A+u v^{\top}\right)$ is not invertible.
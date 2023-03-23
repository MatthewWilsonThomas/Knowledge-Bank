#Mathematics 

### Definition
The Taylor series of a real or complex-valued function $f(x)$ that is infinitely differentiable at a real or complex number $\boldsymbol{a}$ is the power series
$$
f(a)+\frac{f^{\prime}(a)}{1 !}(x-a)+\frac{f^{\prime \prime}(a)}{2 !}(x-a)^2+\frac{f^{\prime \prime \prime}(a)}{3 !}(x-a)^3+\cdots,
$$
where $n$ ! denotes the factorial of $n$. In the more compact sigma notation, this can be written as
$$
\sum_{n=0}^{\infty} \frac{f^{(n)}(a)}{n !}(x-a)^n
$$
where $f^{(n)}(a)$ denotes the $n$-th derivative of $f$ evaluated at the point $a$. (The derivative of order zero of $f$ is defined to be $f$ itself and $(x-a)^0$ and 0 ! are both defined to be 1.)


### Taylor series in several variables
The Taylor series may also be generalised to functions of more than one variable with ${ }^{[14][15]}$
$$
\begin{aligned}
& T\left(x_1, \ldots, x_d\right)= \sum_{n_1=0}^{\infty} \cdots \sum_{n_d=0}^{\infty} \frac{\left(x_1-a_1\right)^{n_1} \cdots\left(x_d-a_d\right)^{n_d}}{n_{1} ! \cdots n_{d} !}\left(\frac{\partial^{n_1+\cdots+n_d} f}{\partial x_1^{n_1} \cdots \partial x_d^{n_d}}\right)\left(a_1, \ldots, a_d\right) \\
&= f\left(a_1, \ldots, a_d\right)+\sum_{j=1}^d \frac{\partial f\left(a_1, \ldots, a_d\right)}{\partial x_j}\left(x_j-a_j\right)+\frac{1}{2 !} \sum_{j=1}^d \sum_{k=1}^d \frac{\partial^2 f\left(a_1, \ldots, a_d\right)}{\partial x_j \partial x_k}\left(x_j-a_j\right)\left(x_k-a_k\right) \\
&+\frac{1}{3 !} \sum_{j=1}^d \sum_{k=1}^d \sum_{l=1}^d \frac{\partial^3 f\left(a_1, \ldots, a_d\right)}{\partial x_j \partial x_k \partial x_l}\left(x_j-a_j\right)\left(x_k-a_k\right)\left(x_l-a_l\right)+\cdots
\end{aligned}
$$
For example, for a function $f(x, y)$ that depends on two variables, $x$ and $y$, the Taylor series to second order about the point $(a, b)$ is
$$
f(a, b)+(x-a) f_x(a, b)+(y-b) f_y(a, b)+\frac{1}{2 !}\left((x-a)^2 f_{x x}(a, b)+2(x-a)(y-b) f_{x y}(a, b)+(y-b)^2 f_{y y}(a, b)\right)
$$
where the subscripts denote the respective partial derivatives.
A second-order Taylor series expansion of a scalar-valued function of more than one variable can be written compactly as
$$
T(\mathbf{x})=f(\mathbf{a})+(\mathbf{x}-\mathbf{a})^{\top} D f(\mathbf{a})+\frac{1}{2 !}(\mathbf{x}-\mathbf{a})^{\top}\left\{D^2 f(\mathbf{a})\right\}(\mathbf{x}-\mathbf{a})+\cdots
$$
where $D f(\mathbf{a})$ is the gradient of $f$ evaluated at $\mathrm{X}=\mathbf{a}$ and $D^2 f(\mathbf{a})$ is the Hessian matrix. Applying the multi-index notation the Taylor series for several variables becomes
$$
T(\mathbf{x})=\sum_{|\alpha| \geq 0} \frac{(\mathbf{x}-\mathbf{a})^\alpha}{\alpha !}\left(\partial^\alpha f\right)(\mathbf{a})
$$
which is to be understood as a still more abbreviated multi-index version of the first equation of this paragraph, with a full analogy to the single variable case.
#Statistics 

Suppose we have multiple outputs $Y_1, Y_2, \ldots, Y_K$ that we wish to predict from our inputs $X_0, X_1, X_2, \ldots, X_p$. We assume a [[Linear Regression]] model for each output
$$
\begin{aligned}
Y_k & =\beta_{0 k}+\sum_{j=1}^p X_j \beta_{j k}+\varepsilon_k \\
& =f_k(X)+\varepsilon_k .
\end{aligned}
$$
With $N$ training cases we can write the model in matrix notation
$$
\mathbf{Y}=\mathbf{X B}+\mathbf{E}
$$
Here $\mathbf{Y}$ is the $N \times K$ response matrix, with $i k$ entry $y_{i k}, \mathbf{X}$ is the $N \times(p+1)$ input matrix, $\mathbf{B}$ is the $(p+1) \times K$ matrix of parameters and $\mathbf{E}$ is the $N \times K$ matrix of errors. A straightforward generalisation of the univariate loss function (3.2) is
$$
\begin{aligned}
\operatorname{RSS}(\mathbf{B}) & =\sum_{k=1}^K \sum_{i=1}^N\left(y_{i k}-f_k\left(x_i\right)\right)^2 \\
& =\operatorname{tr}\left[(\mathbf{Y}-\mathbf{X B})^T(\mathbf{Y}-\mathbf{X B})\right]
\end{aligned}
$$
The [[least squares]] estimates have exactly the same form as before
$$
\hat{\mathbf{B}}=\left(\mathbf{X}^T \mathbf{X}\right)^{-1} \mathbf{X}^T \mathbf{Y}
$$
Hence the coefficients for the $k$-th outcome are just the least squares estimates in the regression of $\mathbf{y}_k$ on $\mathbf{x}_0, \mathbf{x}_1, \ldots, \mathbf{x}_p$. Multiple outputs do not affect one another's least squares estimates.

If the errors $\varepsilon=\left(\varepsilon_1, \ldots, \varepsilon_K\right)$ above are correlated, then it might seem appropriate to modify $RSS(B)$ in favour of a multivariate version. Specifically, suppose $\operatorname{Cov}(\varepsilon)=\boldsymbol{\Sigma}$, then the multivariate weighted criterion
$$
\operatorname{RSS}(\mathbf{B} ; \boldsymbol{\Sigma})=\sum_{i=1}^N\left(y_i-f\left(x_i\right)\right)^T \boldsymbol{\Sigma}^{-1}\left(y_i-f\left(x_i\right)\right)
$$
arises naturally from multivariate Gaussian theory. Here $f(x)$ is the vector function $\left(f_1(x), \ldots, f_K(x)\right)$, and $y_i$ the vector of $K$ responses for observation $i$. However, it can be shown that again the solution is above; $K$ separate regressions that ignore the correlations. If the $\boldsymbol{\Sigma}_i$ vary among observations, then this is no longer the case, and the solution for B no longer decouples.

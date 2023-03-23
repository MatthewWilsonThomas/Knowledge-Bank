#LinearAlgebra 
#Statistics 
An estimation methodology for [[Linear Regression]]
Considering the matrix form of the variables we have:
$$
\operatorname{RSS}(\beta)=(\mathbf{y}-\mathbf{X} \beta)^T(\mathbf{y}-\mathbf{X} \beta)
$$
Differentiating with respect to $\beta$ gives:
$$
\begin{aligned}
\frac{\partial \mathrm{RSS}}{\partial \beta} & =-2 \mathbf{X}^T(\mathbf{y}-\mathbf{X} \beta) \\
\frac{\partial^2 \mathrm{RSS}}{\partial \beta \partial \beta^T} & =2 \mathbf{X}^T \mathbf{X}
\end{aligned}
$$
Assuming (for the moment) that $\mathbf{X}$ has full column rank, and hence $\mathbf{X}^T \mathbf{X}$ is positive definite, we set the first derivative to zero
$$
\mathbf{X}^T(\mathbf{y}-\mathbf{X} \beta)=0
$$
to obtain the unique solution
$$
\hat{\beta}=\left(\mathbf{X}^T \mathbf{X}\right)^{-1} \mathbf{X}^T \mathbf{y}
$$

The predicted values at an input vector $x_0$ are given by $\hat{f}\left(x_0\right)=\left(1: x_0\right)^T \hat{\beta}$; the fitted values at the training inputs are
$$
\hat{\mathbf{y}}=\mathbf{X} \hat{\beta}=\mathbf{X}\left(\mathbf{X}^T \mathbf{X}\right)^{-1} \mathbf{X}^T \mathbf{y}
$$

We can calculate the variance-covariance matrix from the least-squares parameters estimates as:
$$
\operatorname{Var}(\hat{\beta})=\left(\mathbf{X}^T \mathbf{X}\right)^{-1} \sigma^2
$$
Typically one estimates the variance $\sigma^2$ by
$$
\hat{\sigma}^2=\frac{1}{N-p-1} \sum_{i=1}^N\left(y_i-\hat{y}_i\right)^2
$$
The $N-p-1$ rather than $N$ in the denominator makes $\hat{\sigma}^2$ an unbiased estimate of $\sigma^2: \mathrm{E}\left(\hat{\sigma}^2\right)=\sigma^2$.

To draw inferences about the parameters we need further assumptions, i.e. the deviations of $Y$ are additive and Gaussian:
$$
\begin{aligned}
Y & =\mathrm{E}\left(Y \mid X_1, \ldots, X_p\right)+\varepsilon \\
& =\beta_0+\sum_{j=1}^p X_j \beta_j+\varepsilon
\end{aligned}
$$
Using this we can show:
$$
\hat{\beta} \sim N\left(\beta,\left(\mathbf{X}^T \mathbf{X}\right)^{-1} \sigma^2\right)
$$
To test the significance of a particular coefficient we use the z-score:
$$
z_j=\frac{\hat{\beta}_j}{\hat{\sigma} \sqrt{v_j}}
$$
To test the significance of groups of coefficients simultaneously we use the F-stat:
$$
F=\frac{\left(\mathrm{RSS}_0-\mathrm{RSS}_1\right) /\left(p_1-p_0\right)}{\mathrm{RSS}_1 /\left(N-p_1-1\right)}
$$

We can generate a confidence interval around a coefficient as:
$$
\left(\hat{\beta}_j-z^{(1-\alpha)} v_j^{\frac{1}{2}} \hat{\sigma}, \quad \hat{\beta}_j+z^{(1-\alpha)} v_j^{\frac{1}{2}} \hat{\sigma}\right)
$$
We can generate an approximate confidence set for the entire parameter vector $\beta$ as:
$$
C_\beta=\left\{\beta \mid(\hat{\beta}-\beta)^T \mathbf{X}^T \mathbf{X}(\hat{\beta}-\beta) \leq \hat{\sigma}^2 \chi_{p+1}^2(1-\alpha)\right\}
$$

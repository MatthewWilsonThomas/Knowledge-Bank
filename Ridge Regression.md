#Statistics 

Ridge regression is a variant of [[Multivariate Regression]] where we impose a penalty on the coefficients based on their sizes, the penalised residual sum of squares loss function is:$$
\hat{\beta}^{\text {ridge }}=\underset{\beta}{\operatorname{argmin}}\left\{\sum_{i=1}^N\left(y_i-\beta_0-\sum_{j=1}^p x_{i j} \beta_j\right)^2+\lambda \sum_{j=1}^p \beta_j^2\right\}
$$
Equivalently we can write:
$$
\begin{aligned}
& \hat{\beta}^{\text {ridge }}=\underset{\beta}{\operatorname{argmin}} \sum_{i=1}^N\left(y_i-\beta_0-\sum_{j=1}^p x_{i j} \beta_j\right)^2, \\
& \text { subject to } \sum_{j=1}^p \beta_j^2 \leq t,
\end{aligned}
$$

In matrix form this becomes:
$$
\operatorname{RSS}(\lambda)=(\mathbf{y}-\mathbf{X} \beta)^T(\mathbf{y}-\mathbf{X} \beta)+\lambda \beta^T \beta
$$with the coefficients as:
$$
\hat{\beta}^{\text {ridge }}=\left(\mathbf{X}^T \mathbf{X}+\lambda \mathbf{I}\right)^{-1} \mathbf{X}^T \mathbf{y}
$$

Ridge regression has an L2 penalty term. This is a proportional shrinkage towards zero.
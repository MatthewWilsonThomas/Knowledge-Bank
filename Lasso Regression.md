#Statistics 

Lasso regression is a variant of [[Multivariate Regression]] where we impose a penalty on the coefficients based on their sizes, the penalised residual sum of squares loss function is:$$
\hat{\beta}^{\text {1asso }}=\underset{\beta}{\operatorname{argmin}}\left\{\frac{1}{2} \sum_{i=1}^N\left(y_i-\beta_0-\sum_{j=1}^p x_{i j} \beta_j\right)^2+\lambda \sum_{j=1}^p\left|\beta_j\right|\right\}
$$
Equivalently we can write:
$$
\begin{aligned}
\hat{\beta}^{\text {lasso }}= & \underset{\beta}{\operatorname{argmin}} \sum_{i=1}^N\left(y_i-\beta_0-\sum_{j=1}^p x_{i j} \beta_j\right)^2 \\
& \text { subject to } \sum_{j=1}^p\left|\beta_j\right| \leq t .
\end{aligned}
$$


Lasso regression has an L1 penalty term. This makes the solutions non-linear in $y$. Lasso translates each coefficient by a constant factor $\lambda$, truncated at 0, i.e. soft-thresholding. 
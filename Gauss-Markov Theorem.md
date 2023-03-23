#LinearAlgebra 
#Statistics 
A statistical result showing the the [[Least Squares]] estimates of the parameters $\beta$ have the smallest variance among all linear unbiased estimates.

The least squares estimate of $a^T \beta$ is
$$
\hat{\theta}=a^T \hat{\beta}=a^T\left(\mathbf{X}^T \mathbf{X}\right)^{-1} \mathbf{X}^T \mathbf{y}
$$
Considering $\mathbf{X}$ to be fixed, this is a linear function $\mathbf{c}_0^T \mathbf{y}$ of the response vector $\mathbf{y}$. If we assume that the linear model is correct, $a^T \hat{\beta}$ is unbiased since
$$
\begin{aligned}
\mathrm{E}\left(a^T \hat{\beta}\right) & =\mathrm{E}\left(a^T\left(\mathbf{X}^T \mathbf{X}\right)^{-1} \mathbf{X}^T \mathbf{y}\right) \\
& =a^T\left(\mathbf{X}^T \mathbf{X}\right)^{-1} \mathbf{X}^T \mathbf{X} \beta \\
& =a^T \beta
\end{aligned}
$$
The Gauss-Markov theorem states that if we have any other linear estimator $\tilde{\theta}=\mathbf{c}^T \mathbf{y}$ that is unbiased for $a^T \beta$, that is, $\mathrm{E}\left(\mathbf{c}^T \mathbf{y}\right)=a^T \beta$, then
$$
\operatorname{Var}\left(a^T \hat{\beta}\right) \leq \operatorname{Var}\left(\mathbf{c}^T \mathbf{y}\right)
$$
The proof uses the triangle inequality. For simplicity we have stated the result in terms of estimation of a single parameter $a^T \beta$, but with a few more definitions one can state it in terms of the entire parameter vector $\beta$.
Consider the mean squared error of an estimator $\tilde{\theta}$ in estimating $\theta$ :
$$
\begin{aligned}
\operatorname{MSE}(\tilde{\theta}) & =\mathrm{E}(\tilde{\theta}-\theta)^2 \\
& =\operatorname{Var}(\tilde{\theta})+[\mathrm{E}(\tilde{\theta})-\theta]^2
\end{aligned}
$$
The Gauss-Markov theorem implies that the least squares estimator has the smallest mean squared error of all linear estimators with no bias. However, there may well exist a biased estimator with smaller mean squared error.

Mean squared error is intimately related to prediction accuracy. Consider the prediction of the new response at input $x_0$
$$
Y_0=f\left(x_0\right)+\varepsilon_0
$$
Then the expected prediction error of an estimate $\tilde{f}\left(x_0\right)=x_0^T \tilde{\beta}$ is
$$
\begin{aligned}
\mathrm{E}\left(Y_0-\tilde{f}\left(x_0\right)\right)^2 & =\sigma^2+\mathrm{E}\left(x_0^T \tilde{\beta}-f\left(x_0\right)\right)^2 \\
& =\sigma^2+\operatorname{MSE}\left(\tilde{f}\left(x_0\right)\right)
\end{aligned}
$$
Therefore, expected prediction error and mean squared error differ only by the constant $\sigma^2$, representing the variance of the new observation $y_0$.
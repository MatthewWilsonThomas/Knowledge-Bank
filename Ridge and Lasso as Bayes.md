#Statistics 
#BayesianAnalysis 

We can generalise both [[Ridge Regression]] and [[Lasso Regression]] into a form of Bayesian estimates, with the criterion:
$$
\begin{aligned}
\hat{\beta}^{\text {lasso }}= & \underset{\beta}{\operatorname{argmin}} \sum_{i=1}^N\left(y_i-\beta_0-\sum_{j=1}^p x_{i j} \beta_j\right)^2 \\
& \text { subject to } \sum_{j=1}^p\left|\beta_j\right| \leq t .
\end{aligned}
$$
This view allows us to see Ridge and Lasso as Guassian updates on different priors, in Ridge we have a specific given prior and in Lasso we have a Laplacian prior.
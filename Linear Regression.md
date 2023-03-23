#Statistics

The linear regression model has the form:
$$
f(X)=\beta_0+\sum_{j=1}^p X_j \beta_j
$$

The most popular estimation method is [[Least Squares]], in which we minimise:
$$
\begin{aligned}
\operatorname{RSS}(\beta) & =\sum_{i=1}^N\left(y_i-f\left(x_i\right)\right)^2 \\
& =\sum_{i=1}^N\left(y_i-\beta_0-\sum_{j=1}^p x_{i j} \beta_j\right)^2 
\end{aligned}
$$
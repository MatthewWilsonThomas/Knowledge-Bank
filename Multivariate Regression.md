#LinearAlgebra 
#Statistics 

Suppose first that we have a [[Linear Regression]] model with no intercept, that is,
$$
Y=X \beta+\varepsilon
$$
The [[least squares ]]estimate and residuals are
$$
\begin{aligned}
\hat{\beta} & =\frac{\sum_1^N x_i y_i}{\sum_1^N x_i^2}, \\
r_i & =y_i-x_i \hat{\beta} .
\end{aligned}
$$
In convenient vector notation, we let $\mathbf{y}=\left(y_1, \ldots, y_N\right)^T, \mathbf{x}=\left(x_1, \ldots, x_N\right)^T$ and define
$$
\begin{aligned}
\langle\mathbf{x}, \mathbf{y}\rangle & =\sum_{i=1}^N x_i y_i, \\
& =\mathbf{x}^T \mathbf{y},
\end{aligned}
$$the inner product between $\mathbf{x}$ and $\mathbf{y}$. Then we can write
$$
\begin{aligned}
& \hat{\beta}=\frac{\langle\mathbf{x}, \mathbf{y}\rangle}{\langle\mathbf{x}, \mathbf{x}\rangle}, \\
& \mathbf{r}=\mathbf{y}-\mathbf{x} \hat{\beta} .
\end{aligned}
$$
As we will see, this simple univariate regression provides the building block for multiple linear regression. Suppose next that the inputs $\mathbf{x}_1, \mathbf{x}_2, \ldots, \mathbf{x}_p$ (the columns of the data matrix $\mathbf{X}$ ) are orthogonal; that is $\left\langle\mathbf{x}_j, \mathbf{x}_k\right\rangle=0$ for all $j \neq k$. Then it is easy to check that the multiple least squares estimates $\hat{\beta}_j$ are equal to $\left\langle\mathbf{x}_j, \mathbf{y}\right\rangle /\left\langle\mathbf{x}_j, \mathbf{x}_j\right\rangle$-the univariate estimates. In other words, when the inputs are orthogonal, they have no effect on each other's parameter estimates in the model.

Orthogonal inputs occur most often with balanced, designed experiments (where orthogonality is enforced), but almost never with observational data. Hence we will have to orthogonalize them in order to carry this idea further. Suppose next that we have an intercept and a single input $\mathbf{x}$. Then the least squares coefficient of $\mathbf{x}$ has the form
$$
\hat{\beta}_1=\frac{\langle\mathbf{x}-\bar{x} \mathbf{1}, \mathbf{y}\rangle}{\langle\mathbf{x}-\bar{x} \mathbf{1}, \mathbf{x}-\bar{x} \mathbf{1}\rangle}
$$

### Algorithm![[Screenshot 2023-03-02 at 9.21.33 PM.png]]

The result of this algorithm is
$$
\hat{\beta}_p=\frac{\left\langle\mathbf{z}_p, \mathbf{y}\right\rangle}{\left\langle\mathbf{z}_p, \mathbf{z}_p\right\rangle}
$$

We have a corresponding variance of the $\hat{\beta_p}$ $$
\operatorname{Var}\left(\hat{\beta}_p\right)=\frac{\sigma^2}{\left\langle\mathbf{z}_p, \mathbf{z}_p\right\rangle}=\frac{\sigma^2}{\left\|\mathbf{z}_p\right\|^2}
$$
i.e. the precision of our estimates corresponds to the length of the residuals vector.

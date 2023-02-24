#ReinforcementLearning 
[[TD(Lambda) Prediction]]
[[Temporal-Difference]]
[[Monte-Carlo]]
[[RL for Prediction]]

$\lambda$ is a continuous parameter in the range $[0, 1]$ such that $\lambda = 0$ is TD and $\lambda = 1$ is MC. 

### $n$-step Bootstrapping Prediction Algorithm
In TD Value Function update we replace the $G_t$ (from the MC update) with $R_{t+1} + \gamma\cdot V(S_{t+1})$. We can extend this idea further by using the current estimate for the Value Function of the state that is 2 time steps ahead:
$$
V\left(S_t\right) \leftarrow V\left(S_t\right)+\alpha \cdot\left(R_{t+1}+\gamma \cdot R_{t+2}+\gamma^2 \cdot V\left(S_{t+2}\right)-V\left(S_t\right)\right)
$$
This generalises to an update that uses the $n$-step ahead Value Function estimate:
$$
V\left(S_t\right) \leftarrow V\left(S_t\right)+\alpha \cdot\left(G_{t, n}-V\left(S_t\right)\right)
$$
with
$$
\begin{aligned}
G_{t, n} & = \text{$n$-step Bootstrapped Return}\\
& =\sum_{i=t+1}^{t+n} \gamma^{i-t-1} \cdot R_i+\gamma^n \cdot V\left(S_{t+n}\right) \\
& =R_{t+1}+\gamma \cdot R_{t+2}+\gamma^2 \cdot R_{t+3}+\ldots+\gamma^{n-1} \cdot R_{t+n}+\gamma^n \cdot V\left(S_{t+n}\right)
\end{aligned}
$$
To generalise this tabular case to the function approximation case we get the update function as:
$$
\Delta \boldsymbol{w}=\alpha \cdot\left(G_{t, n}-V\left(S_t ; \boldsymbol{w}\right)\right) \cdot \nabla_{\boldsymbol{w}} V\left(S_t ; \boldsymbol{w}\right)
$$
where the new $n$-step bootstrapped return is $G_{t, n}$ is defined in terms of the Function Approximation:
$$
\begin{aligned}
G_{t, n} & =\sum_{i=t+1}^{t+n} \gamma^{i-t-1} \cdot R_i+\gamma^n \cdot V\left(S_{t+n} ; \boldsymbol{w}\right) \\
& =R_{t+1}+\gamma \cdot R_{t+2}+\gamma^2 \cdot R_{t+3}+\ldots+\gamma^{n-1} \cdot R_{t+n}+\gamma^n \cdot V\left(S_{t+n} ; \boldsymbol{w}\right)
\end{aligned}
$$

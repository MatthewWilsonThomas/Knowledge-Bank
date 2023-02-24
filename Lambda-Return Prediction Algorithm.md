#ReinforcementLearning 
[[TD(Lambda) Prediction]]
[[Temporal-Difference]]
[[n-step Bootstrapping Prediction Algorithm]]
[[Monte-Carlo]]
[[RL for Prediction]]
$\lambda$ is a continuous parameter in the range $[0, 1]$ such that $\lambda = 0$ is TD and $\lambda = 1$ is MC. 

### $\lambda$-Return Prediction Algorithm
To extend the $n$-step Bootstrapping Prediction Algorithm to the $\lambda$-Return Prediction Algorithm we alter the $n$-step Bootstrap Target to be a weighted average of its elements:
$$
\sum_{n=1}^N u_n \cdot G_{t, n}+u \cdot G_t \text { where } u+\sum_{n=1}^N u_n=1
$$
This gives us the $\lambda$-Return Target as:
$$
G_t^{(\lambda)}=(1-\lambda) \cdot \sum_{n=1}^{T-t-1} \lambda^{n-1} \cdot G_{t, n}+\lambda^{T-t-1} \cdot G_t
$$
with the new update equation as:
$$
\Delta \boldsymbol{w}=\alpha \cdot\left(G_t^{(\lambda)}-V\left(S_t ; \boldsymbol{w}\right)\right) \cdot \nabla_{\boldsymbol{w}} V\left(S_t ; \boldsymbol{w}\right)
$$

This is an Offline Algorithm as we have to wait till the end of an episode to make an update to the parameters $w$ of the function approximation (rather than making an update after each time step in the episode, i.e. an Online Algorithm)
#ReinforcementLearning 
[[Temporal-Difference]]
[[Monte-Carlo]]
[[RL for Prediction]]

$\lambda$ is a continuous parameter in the range $[0, 1]$ such that $\lambda = 0$ is TD and $\lambda = 1$ is MC. 

### TD($\lambda$) Prediction Algorithm
Based on the [[Eligibility Traces]] the TD($\lambda$) Prediction algorithm performs the following update:
$$V(s) \leftarrow V(s)+\alpha \cdot\left(R_{t+1}+\gamma \cdot V\left(S_{t+1}\right)-V\left(S_t\right)\right) \cdot E_t(s), \text{ for all } s \in \mathcal{N}$$

Then we can update the Value Function for all states at each time step (a generalisation of TD - which only updates the Value Function for the particular state that is visited at that time step), i.e. the update is written as: $$
V(s) \leftarrow V(s)+\alpha \cdot \delta_t \cdot E_t(s), \text { for all } s \in \mathcal{N}
$$
### As an Online $\lambda$-Return Algorithm
This can be seen as the Online version of the $\lambda$-Return Prediction Algorithm as it can be show that if we make all the TD($\lambda$) update offline we are reducing them to the $\lambda$-Return updates.
#### Proof
$$
\sum_{t=0}^{T-1} \alpha \cdot \delta_t \cdot E_t(s)=\sum_{t=0}^{T-1} \alpha \cdot\left(G_t^{(\lambda)}-V\left(S_t\right)\right) \cdot \mathbb{I}_{S_t=s}, \text { for all } s \in \mathcal{N}
$$
where $\mathbb{I}$ denotes the indicator function.
Proof. We begin the proof with the following important identity:
$$
\begin{aligned}
G_t^{(\lambda)}-V\left(S_t\right)=-V\left(S_t\right) & +(1-\lambda) \cdot \lambda^0 \cdot\left(R_{t+1}+\gamma \cdot V\left(S_{t+1}\right)\right) \\
& +(1-\lambda) \cdot \lambda^1 \cdot\left(R_{t+1}+\gamma \cdot R_{t+2}+\gamma^2 \cdot V\left(S_{t+2}\right)\right) \\
& +(1-\lambda) \cdot \lambda^2 \cdot\left(R_{t+1}+\gamma \cdot R_{t+2}+\gamma^2 \cdot R_{t+3}+\gamma^3 \cdot V\left(S_{t+3}\right)\right) \\
& +\ldots \\
=-V\left(S_t\right) & +(\gamma \lambda)^0 \cdot\left(R_{t+1}+\gamma \cdot V\left(S_{t+1}\right)-\gamma \lambda \cdot V\left(S_{t+1}\right)\right) \\
& +(\gamma \lambda)^1 \cdot\left(R_{t+2}+\gamma \cdot V\left(S_{t+2}\right)-\gamma \lambda \cdot V\left(S_{t+2}\right)\right) \\
& +(\gamma \lambda)^2 \cdot\left(R_{t+3}+\gamma \cdot V\left(S_{t+3}\right)-\gamma \lambda \cdot V\left(S_{t+3}\right)\right) \\
& +\ldots \\
& (\gamma \lambda)^0 \cdot\left(R_{t+1}+\gamma \cdot V\left(S_{t+1}\right)-V\left(S_t\right)\right) \\
& +(\gamma \lambda)^1 \cdot\left(R_{t+2}+\gamma \cdot V\left(S_{t+2}\right)-V\left(S_{t+1}\right)\right) \\
& +(\gamma \lambda)^2 \cdot\left(R_{t+3}+\gamma \cdot V\left(S_{t+3}\right)-V\left(S_{t+2}\right)\right) \\
& +\ldots \\
=\quad & \\
=\delta_t+\gamma \lambda \cdot & +(\gamma \lambda)^2 \cdot \delta_{t+2}+\ldots
\end{aligned}
$$
Now assume that a specific non-terminal state $s$ appears at time steps $t_1, t_2, \ldots, t_n$. Then, $$
\begin{aligned}
\sum_{t=0}^{T-1} \alpha \cdot\left(G_t^{(\lambda)}-V\left(S_t\right)\right) \cdot \mathbb{I}_{S_t=s} & =\sum_{i=1}^n \alpha \cdot\left(G_{t_i}^{(\lambda)}-V\left(S_{t_i}\right)\right) \\
& =\sum_{i=1}^n \alpha \cdot\left(\delta_{t_i}+\gamma \lambda \cdot \delta_{t_i+1}+(\gamma \lambda)^2 \cdot \delta_{t_i+2}+\ldots\right) \\
& =\sum_{t=0}^{T-1} \alpha \cdot \delta_t \cdot E_t(s)
\end{aligned}
$$
If we set $\lambda=0$ in this Tabular $\operatorname{TD}(\lambda)$ Prediction algorithm, we note that $E_t(s)$ reduces to $\mathbb{I}_{S_t=s}$ and so, the Tabular $\operatorname{TD}(\lambda)$ prediction algorithm's update for $\lambda=0$ at each time step $t$ reduces to:
$$
V\left(S_t\right) \leftarrow V\left(S_t\right)+\alpha \cdot \delta_t
$$
which is exactly the update of the Tabular TD Prediction algorithm. Therefore, TD algorithms are often referred to as $\mathrm{TD}(0)$.
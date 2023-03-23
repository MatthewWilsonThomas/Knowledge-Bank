#ReinforcementLearning 

Each function approximation in the [[Actor-Critic]] discussion can result in [[Policy Gradient]] algorithms having a bias. This can be overcome with a Compatible Function Approximation.

### Theorem
Let $\boldsymbol{w}_{\boldsymbol{\theta}}^*$ denote the Critic parameters $\boldsymbol{w}$ that minimise the following mean-squared-error for given policy parameters $\boldsymbol{\theta}$ :
$$
\sum_{s \in \mathcal{N}} \rho^\pi(s) \cdot \sum_{a \in \mathcal{A}} \pi(s, a ; \boldsymbol{\theta}) \cdot\left(Q^\pi(s, a)-Q(s, a ; \boldsymbol{w})\right)^2
$$Assume that the data type of $\boldsymbol{\theta}$ is the same as the data type of $\boldsymbol{w}$ and furthermore, assume that for any policy parameters $\boldsymbol{\theta}$, the Critic gradient at $\boldsymbol{w}_{\boldsymbol{\theta}}^*$ is compatible with the Actor score function, i.e.,
$$
\nabla_{\boldsymbol{w}} Q\left(s, a ; \boldsymbol{w}_{\boldsymbol{\theta}}^*\right)=\nabla_{\boldsymbol{\theta}} \log \pi(s, a ; \boldsymbol{\theta}) \text { for all } s \in \mathcal{N}, \text { for all } a \in \mathcal{A}
$$
Then the Policy Gradient using critic $Q\left(s, a ; \boldsymbol{w}_{\boldsymbol{\theta}}^*\right)$ is exact:
$$
\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta})=\sum_{s \in \mathcal{N}} \rho^\pi(s) \cdot \sum_{a \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi(s, a ; \boldsymbol{\theta}) \cdot Q\left(s, a ; \boldsymbol{w}_{\boldsymbol{\theta}}^*\right)
$$
### Proof
For a given $\boldsymbol{\theta}$, since $\boldsymbol{w}_{\boldsymbol{\theta}}^*$ minimises the mean-squared-error as defined above, we have:
$$
\sum_{s \in \mathcal{N}} \rho^\pi(s) \cdot \sum_{a \in \mathcal{A}} \pi(s, a ; \boldsymbol{\theta}) \cdot\left(Q^\pi(s, a)-Q\left(s, a ; \boldsymbol{w}_{\boldsymbol{\theta}}^*\right)\right) \cdot \nabla_{\boldsymbol{w}} Q\left(s, a ; \boldsymbol{w}_{\boldsymbol{\theta}}^*\right)=0
$$
But since $\nabla_{\boldsymbol{w}} Q\left(s, a ; \boldsymbol{w}_{\boldsymbol{\theta}}^*\right)=\nabla_{\boldsymbol{\theta}} \log \pi(s, a ; \boldsymbol{\theta})$, we have:
$$
\sum_{s \in \mathcal{N}} \rho^\pi(s) \cdot \sum_{a \in \mathcal{A}} \pi(s, a ; \boldsymbol{\theta}) \cdot\left(Q^\pi(s, a)-Q\left(s, a ; \boldsymbol{w}_{\boldsymbol{\theta}}^*\right)\right) \cdot \nabla_{\boldsymbol{\theta}} \log \pi(s, a ; \boldsymbol{\theta})=0
$$
Therefore,
$$
\begin{aligned}
& \sum_{s \in \mathcal{N}} \rho^\pi(s) \cdot \sum_{a \in \mathcal{A}} \pi(s, a ; \boldsymbol{\theta}) \cdot Q^\pi(s, a) \cdot \nabla_{\boldsymbol{\theta}} \log \pi(s, a ; \boldsymbol{\theta}) \\
= & \sum_{s \in \mathcal{N}} \rho^\pi(s) \cdot \sum_{a \in \mathcal{A}} \pi(s, a ; \boldsymbol{\theta}) \cdot Q\left(s, a ; \boldsymbol{w}_{\boldsymbol{\theta}}^*\right) \cdot \nabla_{\boldsymbol{\theta}} \log \pi(s, a ; \boldsymbol{\theta})
\end{aligned}
$$
$$
\text { But } \nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta})=\sum_{s \in \mathcal{N}} \rho^\pi(s) \cdot \sum_{a \in \mathcal{A}} \pi(s, a ; \boldsymbol{\theta}) \cdot Q^\pi(s, a) \cdot \nabla_{\boldsymbol{\theta}} \log \pi(s, a ; \boldsymbol{\theta})
$$
So, $\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta})=\sum_{s \in \mathcal{N}} \rho^\pi(s) \cdot \sum_{a \in \mathcal{A}} \pi(s, a ; \boldsymbol{\theta}) \cdot Q\left(s, a ; \boldsymbol{w}_{\boldsymbol{\theta}}^*\right) \cdot \nabla_{\boldsymbol{\theta}} \log \pi(s, a ; \boldsymbol{\theta})$
$$
=\sum_{s \in \mathcal{N}} \rho^\pi(s) \cdot \sum_{a \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi(s, a ; \boldsymbol{\theta}) \cdot Q\left(s, a ; \boldsymbol{w}_{\boldsymbol{\theta}}^*\right)
$$
$\mathbb{Q} \cdot \mathbb{E} \cdot \mathbb{D}$


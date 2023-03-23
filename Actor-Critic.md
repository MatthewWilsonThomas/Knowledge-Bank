#ReinforcementLearning 

A simple way to reduce the variance of [[Monte-Carlo]] methods is to use a function approximation for the Q-Value Function instead of the trace experience return as an unbiased sample of the Q-Value Function. This causes variance reduction as a function approximation will update gradually (gradient descent). We now have two function approximations in this algorithm:
- $\pi(s, a;\theta)$ as the Actor.
- $Q(s,a;\omega)$ as the Critic
These approximations collaborate to improve the policy using gradient descent. Intuitively, the Actor updates the parameters in a direction suggested by the Critic.

We calculate the gradient of $J(\theta)$ using 'approximate gradient descent' (some bias is introduced by using the Critic for guidance):
$$
\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta}) \approx \sum_{s \in \mathcal{N}} \rho^\pi(s) \cdot \sum_{a \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi(s, a ; \boldsymbol{\theta}) \cdot Q(s, a ; \boldsymbol{w})
$$

We can further reduce the variance of Actor-Critics by subtracting a Baseline Function $B(s)$ in the [[Policy Gradient]] estimate. The parameter update then becomes:
$$
\Delta \boldsymbol{\theta}=\alpha \cdot \gamma^t \cdot \nabla_{\boldsymbol{\theta}} \log \pi\left(S_t, A_t ; \boldsymbol{\theta}\right) \cdot\left(Q\left(S_t, A_t ; \boldsymbol{w}\right)-B\left(S_t\right)\right)
$$
(we must have the Baseline as only a function of the state (s) so that it doesn't add any bias to this estimate). 
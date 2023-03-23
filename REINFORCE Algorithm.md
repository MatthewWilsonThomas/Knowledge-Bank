#ReinforcementLearning 

REINFORCE is one of the simplest [[Policy Gradient]] Algorithms. It uses the trace experience return of $G_t$ for $(S_t, A_t)$ while following the policy $\pi$ as an unbiased sample of $Q^\pi(S_t, A_t)$, thus for every time step of each episode we estimate $\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta})$ by calculating $\gamma^t \cdot\left(\nabla_{\boldsymbol{\theta}} \log \pi\left(S_t, A_t ; \boldsymbol{\theta}\right)\right) \cdot G_t$. The parameter update (utilising stochastic gradient descent) becomes:
$$
\Delta \boldsymbol{\theta}=\alpha \cdot \gamma^t \cdot\left(\nabla_{\boldsymbol{\theta}} \log \pi\left(S_t, A_t ; \boldsymbol{\theta}\right)\right) \cdot G_t
$$
This Policy Gradient algorithm is is [[Monte-Carlo]] since it is not bootstrapped (i.e. it uses the full trace experience). In our classification this is a Policy-based algorithm as it doesn't involve learning the Value Function of the MDP. 

The [[Score Function]] in this case is given as
$$
\nabla_{\boldsymbol{\theta}} \log \pi(s, a ; \boldsymbol{\theta})=\frac{(a-g(s ; \boldsymbol{\theta})) \cdot \nabla_{\boldsymbol{\theta}} g(s ; \boldsymbol{\theta})}{\sigma^2}
$$
 
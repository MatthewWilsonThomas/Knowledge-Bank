#ReinforcementLearning 

This is a class of algorithms to solve [[Markov Decision Process]] Control problems. 

These are not technically RL algorithms. 
Evolutionary Strategies (abbreviated as ES) actually refers to a technique/approach that is best understood as a type of Black-Box Optimisation. It was popularised in the 1970s as Heuristic Search Methods. It is loosely inspired by natural evolution of living beings. We focus on a subclass of ES known as Natural Evolutionary Strategies (abbreviated as NES).

The original setting for this approach was quite generic and not at all specific to solving MDPs. Let us understand this generic setting first. Given an objective function $F(\psi)$, where $\psi$ refers to parameters, we consider a probability distribution $p_\theta(\psi)$ over $\psi$, where $\theta$ refers to the parameters of the probability distribution. The goal in this generic setting is to maximise the average objective $\mathbb{E}_{\psi \sim p_\theta}[F(\psi)]$. We search for optimal $\theta$ with stochastic gradient ascent as follows:
$$
\begin{aligned}
\nabla_{\boldsymbol{\theta}}\left(\mathbb{E}_{\boldsymbol{\psi} \sim p_\theta}[F(\boldsymbol{\psi})]\right) & =\nabla_{\boldsymbol{\theta}}\left(\int_{\boldsymbol{\psi}} p_{\boldsymbol{\theta}}(\boldsymbol{\psi}) \cdot F(\boldsymbol{\psi}) \cdot d \boldsymbol{\psi}\right) \\
& =\int_\psi \nabla_{\boldsymbol{\theta}}\left(p_{\boldsymbol{\theta}}(\boldsymbol{\psi})\right) \cdot F(\boldsymbol{\psi}) \cdot d \boldsymbol{\psi} \\
& =\int_\psi p_{\boldsymbol{\theta}}(\boldsymbol{\psi}) \cdot \nabla_{\boldsymbol{\theta}}\left(\log p_{\boldsymbol{\theta}}(\boldsymbol{\psi})\right) \cdot F(\boldsymbol{\psi}) \cdot d \boldsymbol{\psi} \\
& =\mathbb{E}_{\psi \sim p_\theta}\left[\nabla_{\boldsymbol{\theta}}\left(\log p_{\boldsymbol{\theta}}(\boldsymbol{\psi})\right) \cdot F(\boldsymbol{\psi})\right]
\end{aligned}
$$
Now let's see how NES can be applied to solving MDP Control. We set $F(\cdot)$ to be the (stochastic) Return of an MDP. $\psi$ corresponds to the parameters of a deterministic policy $\pi_\psi: \mathcal{N} \rightarrow \mathcal{A}$. $\psi \in \mathbb{R}^m$ is drawn from an isotropic $m$-variate Gaussian distribution, i.e., Gaussian with mean vector $\boldsymbol{\theta} \in \mathbb{R}^m$ and fixed diagonal covariance matrix $\sigma^2 \boldsymbol{I}_m$ where $\sigma \in \mathbb{R}$ is kept fixed and $\boldsymbol{I}_m$ is the $m \times m$ identity matrix. The average objective (Expected Return) can then be written as:
$$
\mathbb{E}_{\psi \sim p_\theta}[F(\boldsymbol{\psi})]=\mathbb{E}_{\boldsymbol{\epsilon} \sim \mathcal{N}\left(0, I_m\right)}[F(\boldsymbol{\theta}+\sigma \cdot \boldsymbol{\epsilon})]
$$
where $\epsilon \in \mathbb{R}^m$ is the standard normal random variable generating $\psi$. Hence, from the Equation above,  the gradient $\left(\nabla_\theta\right)$ of Expected Return can be written as:
$$
\begin{gathered}
\mathbb{E}_{\psi \sim p_{\boldsymbol{\theta}}}\left[\nabla_{\boldsymbol{\theta}}\left(\log p_{\boldsymbol{\theta}}(\boldsymbol{\psi})\right) \cdot F(\boldsymbol{\psi})\right] \\
=\mathbb{E}_{\boldsymbol{N} \sim\left(\boldsymbol{\theta}, \sigma^2 \boldsymbol{I}_m\right)}\left[\nabla_{\boldsymbol{\theta}}\left(\frac{-(\boldsymbol{\psi}-\boldsymbol{\theta})^T \cdot(\boldsymbol{\psi}-\boldsymbol{\theta})}{2 \sigma^2}\right) \cdot F(\boldsymbol{\psi})\right] \\
=\frac{1}{\sigma} \cdot \mathbb{E}_{\boldsymbol{\epsilon} \sim \mathcal{N}\left(0, \boldsymbol{I}_{\boldsymbol{m}}\right)}[\boldsymbol{\epsilon} \cdot F(\boldsymbol{\theta}+\sigma \cdot \boldsymbol{\epsilon})]
\end{gathered}
$$

Now we come up with a sampling-based algorithm to solve the MDP. The above formula helps estimate the gradient of Expected Return by sampling several $\epsilon$ (each $\epsilon$ represents a Policy $\left.\pi_{\theta+\sigma \cdot \epsilon}\right)$, and averaging $\epsilon \cdot F(\boldsymbol{\theta}+\sigma \cdot \boldsymbol{\epsilon})$ across a large set $(n)$ of $\epsilon$ samples.

Note that evaluating $F(\theta+\sigma \cdot \boldsymbol{\epsilon})$ involves playing an episode for a given sampled $\epsilon$, and obtaining that episode's Return $F(\boldsymbol{\theta}+\sigma \cdot \boldsymbol{\epsilon})$. Hence, we have $n$ values of $\boldsymbol{\epsilon}, n$ Policies $\pi_{\boldsymbol{\theta}+\sigma \cdot \epsilon}$, and $n$ Returns $F(\boldsymbol{\theta}+\sigma \cdot \boldsymbol{\epsilon})$.

Given the gradient estimate, we update $\theta$ in this gradient direction, which in turn leads to new samples of $\epsilon$ (new set of Policies $\pi_{\theta+\sigma \cdot \epsilon}$ ), and the process repeats until $\mathbb{E}_{\boldsymbol{\epsilon} \sim \mathcal{N}\left(0, \boldsymbol{I}_m\right)}[F(\boldsymbol{\theta}+\sigma \cdot \boldsymbol{\epsilon})]$ is maximized.
The key inputs to the algorithm are:
- Learning rate (SGD Step Size) $\alpha$
- Standard Deviation $\sigma$
- Initial value of parameter vector $\theta_0$
With these inputs, for each iteration $t=0,1,2, \ldots$, the algorithm performs the following steps:
- Sample $\epsilon_1, \epsilon_2, \ldots \epsilon_n \sim \mathcal{N}\left(0, I_m\right)$.
- Compute Returns $F_i \leftarrow F\left(\boldsymbol{\theta}_t+\sigma \cdot \epsilon_i\right)$ for $i=1,2, \ldots, n$.
- $\theta_{t+1} \leftarrow \theta_t+\frac{\alpha}{n \sigma} \sum_{i=1}^n \epsilon_i \cdot F_i$
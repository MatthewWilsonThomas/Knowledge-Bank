#ReinforcementLearning 
#Statistics 

Here we detail a few of the analytically derived canonical Score Functions

### Canonical $\pi(s, a ; \boldsymbol{\theta})$ for Finite Action Spaces
For finite action spaces, we often use the Softmax Policy. Assume $\theta$ is an $m$-vector $\left(\theta_1, \ldots, \theta_m\right)$ and assume feature vector $\phi(s, a)$ is given by: $\left(\phi_1(s, a), \ldots, \phi_m(s, a)\right)$ for all $s \in \mathcal{N}, a \in \mathcal{A}$. We weight actions using linear combinations of features, i.e., $\boldsymbol{\phi}(s, a)^T \cdot \boldsymbol{\theta}$, and we set the action probabilities to be proportional to exponentiated weights, as follows:
$$
\pi(s, a ; \boldsymbol{\theta})=\frac{e^{\boldsymbol{\phi ( s , a ) ^ { T } \cdot \boldsymbol { \theta }}}}{\sum_{b \in \mathcal{A}} e^{\boldsymbol{\phi}(s, b)^T \cdot \boldsymbol{\theta}}} \text { for all } s \in \mathcal{N}, a \in \mathcal{A}
$$
Then the score function is given by:
$$
\nabla_{\boldsymbol{\theta}} \log \pi(s, a ; \boldsymbol{\theta})=\boldsymbol{\phi}(s, a)-\sum_{b \in \mathcal{A}} \pi(s, b ; \boldsymbol{\theta}) \cdot \boldsymbol{\phi}(s, b)=\boldsymbol{\phi}(s, a)-\mathbb{E}_\pi[\boldsymbol{\phi}(s, \cdot)]
$$
The intuitive interpretation is that the score function for an action $a$ represents the "advantage" of the feature vector for action $a$ over the mean feature vector (across all actions), for a given state $s$.

### Canonical $\pi(s, a ; \boldsymbol{\theta})$ for Single-Dimensional Continuous Action Spaces
For single-dimensional continuous action spaces (i.e., $\mathcal{A}=\mathbb{R}$ ), we often use a Gaussian distribution for the Policy. Assume $\boldsymbol{\theta}$ is an $m$-vector $\left(\theta_1, \ldots, \theta_m\right)$ and assume the state features vector $\phi(s)$ is given by $\left(\phi_1(s), \ldots, \phi_m(s)\right)$ for all $s \in \mathcal{N}$.

We set the mean of the Gaussian distribution for the Policy as a linear combination of state features, i.e., $\phi(s)^T \cdot \boldsymbol{\theta}$, and we set the variance to be a fixed value, say $\sigma^2$. We could make the variance parameterised as well, but let's work with fixed variance to keep things simple.
The Gaussian policy selects an action $a$ as follows:
$a \sim \mathcal{N}\left(\phi(s)^T \cdot \boldsymbol{\theta}, \sigma^2\right)$ for a given $s \in \mathcal{N}$
Then the score function is given by:
$$
\nabla_{\boldsymbol{\theta}} \log \pi(s, a ; \boldsymbol{\theta})=\frac{\left(a-\boldsymbol{\phi}(s)^T \cdot \boldsymbol{\theta}\right) \cdot \boldsymbol{\phi}(s)}{\sigma^2}
$$
This is easily extensible to multi-dimensional continuous action spaces by considering a multi-dimensional Gaussian distribution for the Policy.

The intuitive interpretation is that the score function for an action $a$ is proportional to the feature vector for given state $s$ scaled by the "advantage" of the action $a$ over the mean action (note: each $a \in \mathbb{R}$ ).

For each of the above two examples (finite action spaces and continuous action spaces), think of the "features advantage" of an action as the compass for the Gradient Ascent. The gradient estimate for an encountered action is proportional to the action's "features advantage" scaled by the action's Value Function. The intuition is that the Gradient Ascent encourages picking actions that are yielding more favorable outcomes (Policy Improvement) so as to ultimately get to a point where the optimal action is selected for each state.
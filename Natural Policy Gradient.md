#ReinforcementLearning 
A [[Policy Gradient]] algorithm that works in practice.

The core motivation is that when the parameter space has a certain underlying structure, the usual gradient doesn't represent the steepest descent direction, the Natural Gradient does. 

 The steepest descent direction of an arbitrary function $f(\theta)$ to be minimised is defined as the vector $\Delta \theta$ that minimises $f(\theta+\Delta \theta)$ under the constraint that the length $|\Delta \theta|$ is a constant. In general, the length $|\Delta \theta|$ is defined with respect to some positive-definite matrix $G(\theta)$ governed by the underlying structure of the $\theta$ parameters space, i.e.,
$$
|\Delta \boldsymbol{\theta}|^2=(\Delta \boldsymbol{\theta})^T \cdot \boldsymbol{G}(\boldsymbol{\theta}) \cdot \Delta \boldsymbol{\theta}
$$
We can show that under the length metric defined by the matrix $G$, the steepest descent direction is:$$
\nabla_{\boldsymbol{\theta}}^{\text {nat }} f(\boldsymbol{\theta})=\boldsymbol{G}^{-1}(\boldsymbol{\theta}) \cdot \nabla_{\boldsymbol{\theta}} f(\boldsymbol{\theta})
$$
We refer to this steepest descent direction $\nabla_\theta^{\text {nat }} f(\theta)$ as the Natural Gradient. We can update the parameters $\theta$ in this Natural Gradient direction in order to achieve steepest descent (according to the matrix $G$ ), as follows:
$$
\Delta \theta=-\alpha \cdot \nabla_{\boldsymbol{\theta}}^{\text {nat }} f(\boldsymbol{\theta})
$$
Specialising this to the case of the Expected Return function $J(\theta)$ we get the results:
$$
\nabla_{\boldsymbol{\theta}}^{\text {nat }} J(\boldsymbol{\theta})=\boldsymbol{w}_\theta^*
$$
This compact result enables a simple algorithm for Natural Policy Gradient (NPG):
- After each atomic experience, update Critic parameters $w$ with the critic loss gradient as:
$$
\Delta \boldsymbol{w}=\alpha_{\boldsymbol{w}} \cdot\left(R_{t+1}+\gamma \cdot \boldsymbol{S} \boldsymbol{C}\left(S_{t+1}, A_{t+1} ; \boldsymbol{\theta}\right)^T \cdot \boldsymbol{w}-\boldsymbol{S} \boldsymbol{C}\left(S_t, A_t ; \boldsymbol{\theta}\right)^T \cdot \boldsymbol{w}\right) \cdot \boldsymbol{S} \boldsymbol{C}\left(S_t, A_t ; \boldsymbol{\theta}\right)
$$
- After each atomic experience, update Actor parameters $\theta$ in the direction of $\boldsymbol{w}$ :
$$
\Delta \theta=\alpha_\theta \cdot \boldsymbol{w}
$$

#ReinforcementLearning 
Policy Gradient takes a different approach to the previous algorithms as they are not based on consulting the Q-Value Function. These algorithms try to find the Policy which results in the Best Expected Returns, i.e. performing Gradient Ascent on the Expected Returns, with respect to the parameters of a Policy [[function approximation]]. 

This gives rise to the [[Actor-Critic]] collaboration

### Policy Gradient Theorem
Expected Returns Objective $J(\boldsymbol{\theta})$:
$$
J(\boldsymbol{\theta})=\mathbb{E}_\pi\left[\sum_{t=0}^{\infty} \gamma^t \cdot R_{t+1}\right]
$$
Value Function $V^\pi(s)$ and Action Value function $Q^\pi(s, a)$ are defined as:
$$
\begin{gathered}
V^\pi(s)=\mathbb{E}_\pi\left[\sum_{k=t}^{\infty} \gamma^{k-t} \cdot R_{k+1} \mid S_t=s\right] \text { for all } t=0,1,2, \ldots \\
Q^\pi(s, a)=\mathbb{E}_\pi\left[\sum_{k=t}^{\infty} \gamma^{k-t} \cdot R_{k+1} \mid S_t=s, A_t=a\right] \text { for all } t=0,1,2, \ldots
\end{gathered}
$$
We define the Advantage Function as:
$$
A^\pi(s, a)=Q^\pi(s, a)-V^\pi(s)
$$ the advantage function captures how much more value a particular action provides relative to the average value across actions. 

The Expected Returns objective can be expressed as:
$$
\begin{gathered}
J(\boldsymbol{\theta})=\mathbb{E}_\pi\left[\sum_{t=0}^{\infty} \gamma^t \cdot R_{t+1}\right]=\sum_{t=0}^{\infty} \gamma^t \cdot \mathbb{E}_\pi\left[R_{t+1}\right] \\
=\sum_{t=0}^{\infty} \gamma^t \cdot \sum_{s \in \mathcal{N}}\left(\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot p\left(S_0 \rightarrow s, t, \pi\right)\right) \cdot \sum_{a \in \mathcal{A}} \pi(s, a ; \boldsymbol{\theta}) \cdot \mathcal{R}_s^a \\
=\sum_{s \in \mathcal{N}}\left(\sum_{S_0 \in \mathcal{N}} \sum_{t=0}^{\infty} \gamma^t \cdot p_0\left(S_0\right) \cdot p\left(S_0 \rightarrow s, t, \pi\right)\right) \cdot \sum_{a \in \mathcal{A}} \pi(s, a ; \boldsymbol{\theta}) \cdot \mathcal{R}_s^a
\end{gathered}
$$
Giving the definition of $\rho^\pi(s)$ as the Discounted Aggregate State Visitation measure:
$$
J(\boldsymbol{\theta})=\sum_{s \in \mathcal{N}} \rho^\pi(s) \cdot \sum_{a \in \mathcal{A}} \pi(s, a ; \boldsymbol{\theta}) \cdot \mathcal{R}_s^a
$$
where
$$
\rho^\pi(s)=\sum_{S_0 \in \mathcal{N}} \sum_{t=0}^{\infty} \gamma^t \cdot p_0\left(S_0\right) \cdot p\left(S_0 \rightarrow s, t, \pi\right)
$$
$\rho^\pi(s)$ is a measure over the set of non-terminal states (but not a probability measure). 


#### Statement
$$
\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta})=\sum_{s \in \mathcal{N}} \rho^\pi(s) \cdot \sum_{a \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi(s, a ; \boldsymbol{\theta}) \cdot Q^\pi(s, a)
$$
#### Proof
We begin the proof by noting that:
$$
J(\boldsymbol{\theta})=\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot V^\pi\left(S_0\right)=\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot \sum_{A_0 \in \mathcal{A}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot Q^\pi\left(S_0, A_0\right)
$$
Calculate $\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta})$ by its product parts $\pi\left(S_0, A_0 ; \boldsymbol{\theta}\right)$ and $Q^\pi\left(S_0, A_0\right)$.
$$
\begin{aligned}
\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta}) & =\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot \sum_{A_0 \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot Q^\pi\left(S_0, A_0\right) \\
& +\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot \sum_{A_0 \in \mathcal{A}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot \nabla_{\boldsymbol{\theta}} Q^\pi\left(S_0, A_0\right)
\end{aligned}
$$
Now expand $Q^\pi\left(S_0, A_0\right)$ as:
$$
\begin{aligned}
& \mathcal{R}_{S_0}^{A_0}+\sum_{S_1 \in \mathcal{N}} \gamma \cdot \mathcal{P}_{S_0, S_1}^{A_0} \cdot V^\pi\left(S_1\right) \text { (Bellman Policy Equation) } \\
\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta}) & =\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot \sum_{A_0 \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot Q^\pi\left(S_0, A_0\right) \\
& +\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot \sum_{A_0 \in \mathcal{A}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot \nabla_{\boldsymbol{\theta}}\left(\mathcal{R}_{S_0}^{A_0}+\sum_{S_1 \in \mathcal{N}} \gamma \cdot \mathcal{P}_{S_0, S_1}^{A_0} \cdot V^\pi\left(S_1\right)\right)
\end{aligned}
$$
Note: $\nabla_\theta \mathcal{R}_{S_0}^{A_0}=0$, so remove that term.
$$
\begin{aligned}
\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta}) & =\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot \sum_{A_0 \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot Q^\pi\left(S_0, A_0\right) \\
& +\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot \sum_{A_0 \in \mathcal{A}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot \nabla_{\boldsymbol{\theta}}\left(\sum_{S_1 \in \mathcal{N}} \gamma \cdot \mathcal{P}_{S_0, S_1}^{A_0} \cdot V^\pi\left(S_1\right)\right)
\end{aligned}
$$
Now bring the $\nabla_{\boldsymbol{\theta}}$ inside the $\sum_{S_1 \in \mathcal{N}}$ to apply only on $V^\pi\left(S_1\right)$.
$$
\begin{aligned}
\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta}) & =\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot \sum_{A_0 \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot Q^\pi\left(S_0, A_0\right) \\
& +\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot \sum_{A_0 \in \mathcal{A}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot \sum_{S_1 \in \mathcal{N}} \gamma \cdot \mathcal{P}_{S_0, S_1}^{A_0} \cdot \nabla_{\boldsymbol{\theta}} V^\pi\left(S_1\right)
\end{aligned}
$$
Now bring $\sum_{S_0 \in \mathcal{N}}$ and $\sum_{A_0 \in \mathcal{A}}$ inside the $\sum_{S_1 \in \mathcal{N}}$
$$
\begin{gathered}
\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta})=\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot \sum_{A_0 \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot Q^\pi\left(S_0, A_0\right) \\
+\sum_{S_1 \in \mathcal{N}} \sum_{S_0 \in \mathcal{N}} \gamma \cdot p_0\left(S_0\right) \cdot\left(\sum_{A_0 \in \mathcal{A}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot \mathcal{P}_{S_0, S_1}^{A_0}\right) \cdot \nabla_{\boldsymbol{\theta}} V^\pi\left(S_1\right) \\
\text { Note that } \sum_{A_0 \in \mathcal{A}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot \mathcal{P}_{S_0, S_1}^{A_0}=p\left(S_0 \rightarrow S_1, 1, \pi\right) \\
\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta})=\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot \sum_{A_0 \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot Q^\pi\left(S_0, A_0\right) \\
\quad+\sum_{S_1 \in \mathcal{N}} \sum_{S_0 \in \mathcal{N}} \gamma \cdot p_0\left(S_0\right) \cdot p\left(S_0 \rightarrow S_1, 1, \pi\right) \cdot \nabla_{\boldsymbol{\theta}} V^\pi\left(S_1\right) \\
\text { Now } \operatorname{expand} V^\pi\left(S_1\right) \text { to } \sum_{A_1 \in \mathcal{A}} \pi\left(S_1, A_1 ; \boldsymbol{\theta}\right) \cdot Q^\pi\left(S_1, A_1\right) \\
\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta})=\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot \sum_{A_0 \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot Q^\pi\left(S_0, A_0\right) \\
+\sum_{S_1 \in \mathcal{N}} \sum_{S_0 \in \mathcal{N}} \gamma \cdot p_0\left(S_0\right) \cdot p\left(S_0 \rightarrow S_1, 1, \pi\right) \cdot \nabla_{\boldsymbol{\theta}}\left(\sum_{A_1 \in \mathcal{A}} \pi\left(S_1, A_1 ; \boldsymbol{\theta}\right) \cdot Q^\pi\left(S_1, A_1\right)\right)
\end{gathered}
$$
We are now back to when we started calculating gradient of $\sum_a \pi \cdot Q^\pi$. Follow the same process of calculating the gradient of $\pi \cdot Q^\pi$ by parts, then Bellman-expanding $Q^\pi$ (to calculate its gradient), and iterate.
$$
\begin{gathered}
\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta})=\sum_{S_0 \in \mathcal{N}} p_0\left(S_0\right) \cdot \sum_{A_0 \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi\left(S_0, A_0 ; \boldsymbol{\theta}\right) \cdot Q^\pi\left(S_0, A_0\right)+ \\
\sum_{S_1 \in \mathcal{N}} \sum_{S_0 \in \mathcal{N}} \gamma \cdot p_0\left(S_0\right) \cdot p\left(S_0 \rightarrow S_1, 1, \pi\right) \cdot\left(\sum_{A_1 \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi\left(S_1, A_1 ; \boldsymbol{\theta}\right) \cdot Q^\pi\left(S_1, A_1\right)+\ldots\right)
\end{gathered}
$$
This iterative process leads us to:
$$
\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta})=\sum_{t=0}^{\infty} \sum_{S_t \in \mathcal{N}} \sum_{S_0 \in \mathcal{N}} \gamma^t \cdot p_0\left(S_0\right) \cdot p\left(S_0 \rightarrow S_t, t, \pi\right) \cdot \sum_{A_t \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi\left(S_t, A_t ; \boldsymbol{\theta}\right) \cdot Q^\pi\left(S_t, A_t\right)
$$
Bring $\sum_{t=0}^{\infty}$ inside $\sum_{S_t \in \mathcal{N}} \sum_{S_0 \in \mathcal{N}}$ and note that
$$
\begin{gathered}
\sum_{A_t \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi\left(S_t, A_t ; \boldsymbol{\theta}\right) \cdot Q^\pi\left(S_t, A_t\right) \text { is independent of } t \\
\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta})=\sum_{s \in \mathcal{N}} \sum_{S_0 \in \mathcal{N}} \sum_{t=0}^{\infty} \gamma^t \cdot p_0\left(S_0\right) \cdot p\left(S_0 \rightarrow s, t, \pi\right) \cdot \sum_{a \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi(s, a ; \boldsymbol{\theta}) \cdot Q^\pi(s, a) \\
\text { Remember that } \sum_{S_0 \in \mathcal{N}} \sum_{t=0}^{\infty} \gamma^t \cdot p_0\left(S_0\right) \cdot p\left(S_0 \rightarrow s, t, \pi\right) \stackrel{\text { def }}{=} \rho^\pi(s) . \text { So, } \\
\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta})=\sum_{s \in \mathcal{N}} \rho^\pi(s) \cdot \sum_{a \in \mathcal{A}} \nabla_{\boldsymbol{\theta}} \pi(s, a ; \boldsymbol{\theta}) \cdot Q^\pi(s, a)
\end{gathered}
$$
$\mathbb{Q} \cdot \mathbb{E} \cdot \mathbb{D}$.
As explained earlier, since the state occurrence probabilities and action occurrence probabilities are implicit in the trace experiences, we can sample-estimate $\nabla_\theta J(\theta)$ by calculating $\gamma^t \cdot\left(\nabla_{\boldsymbol{\theta}} \log \pi\left(S_t, A_t ; \boldsymbol{\theta}\right)\right) \cdot Q^\pi\left(S_t, A_t\right)$ at each time step in each trace experience, and update the parameters $\boldsymbol{\theta}$ (according to Stochastic Gradient Ascent) with this calculation.
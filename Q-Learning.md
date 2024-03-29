#ReinforcementLearning 

The most basic [[Off-Policy Control]] category of algorithm within [[RL for Control]] algorithms is Q-Learning. 

The best way to understand the (Off-Policy) Q-Learning algorithm is to tweak SARSA to make it Off-Policy. Instead of having both the action $A$ and the next action $A^{\prime}$ being generated by the same $\epsilon$-greedy policy, we generate (i.e., sample) action $A$ (from state $S$ ) using an exploratory behaviour policy $\mu$ and we generate the next action $A^{\prime}$ (from next state $\left.S^{\prime}\right)$ using the target policy $\pi$. The behaviour policy can be any policy as long as it is exploratory enough to be able to obtain sufficient data for all actions (in order to obtain an adequate estimate of the $Q$-Value Function). Note that in SARSA, when we roll over to the next (new) time step, the new time step's state $S$ is set to be equal to the previous time step's next state $S^{\prime}$ and the new time step's action $A$ is set to be equal to the previous time step's next action $A^{\prime}$. However, in Q-Learning, we only set the new time step's state $S$ to be equal to the previous time step's next state $S^{\prime}$. The action $A$ for the new time step will be generated using the behaviour policy $\mu$, and won't be equal to the previous time step's next action $A^{\prime}$ (that would have been generated using the target policy $\pi$ ).

This Q-Learning idea of two separate policies-behaviour policy and target policy-is fairly generic, and can be used in algorithms beyond solving the Control problem. However, here we are interested in $Q$-Learning for Control and so, we want to ensure that the target policy eventually becomes the optimal policy. One straightforward way to accomplish this is to make the target policy equal to the deterministic greedy policy derived from the Q-Value Function estimate at every step. Thus, the update for Q-Learning Control algorithm is as follows:
$$
\Delta \boldsymbol{w}=\alpha \cdot \delta_t \cdot \nabla_{\boldsymbol{w}} Q\left(S_t, A_t ; \boldsymbol{w}\right)
$$
where
$$
\begin{aligned}
\delta_t & =R_{t+1}+\gamma \cdot Q\left(S_{t+1}, \underset{a \in \mathcal{A}}{\arg \max } Q\left(S_{t+1}, a ; \boldsymbol{w}\right) ; \boldsymbol{w}\right)-Q\left(S_t, A_t ; \boldsymbol{w}\right) \\
& =R_{t+1}+\gamma \cdot \max _{a \in \mathcal{A}} Q\left(S_{t+1}, a ; \boldsymbol{w}\right)-Q\left(S_t, A_t ; \boldsymbol{w}\right)
\end{aligned}
$$

Although we have highlighted some attractive features of Q-Learning (on account of be- ing Off-Policy), it turns out that Q-Learning when combined with function approximation of the Q-Value Function leads to convergence issues (more on this later). However, Tabular Q-Learning converges under the usual appropriate conditions. There is considerable literature on convergence of Tabular Q-Learning and we won’t go over those convergence theorems in this book, here it suﬀices to say that the convergence proofs for Tabular Q-Learning require infinite exploration of all (state, action) pairs and appropriate stochastic approximation conditions for step sizes.
#Algorithm 
#ReinforcementLearning 
#Planning

This is a [[Dynamic Programming]] algorithm used for [[Markov Decision Process]] optimisation.

### Optimal Policy from Optimal Value Function
Value Iteration does not deal with any policies, only the value functions. This means that we extract an optimal policy from the optimal value function s.t. $V^{\pi^*} = V^*$. We can do this using the Greedy Policy function $G$:
$$

\boldsymbol{B}^{G(\boldsymbol{V})}(\boldsymbol{V})=\boldsymbol{B}^*(\boldsymbol{V}) \text { for all } \boldsymbol{V} \in \mathbb{R}^m

$$Specialising $\boldsymbol{V}$ to $\boldsymbol{V}^*$, we get:
$$

\boldsymbol{B}^{G\left(\boldsymbol{V}^*\right)}\left(\boldsymbol{V}^*\right)=\boldsymbol{B}^*\left(\boldsymbol{V}^*\right)

$$
But we know $\boldsymbol{V}^*$ is the Fixed-Point of $\boldsymbol{B}^*$, i.e., $\boldsymbol{B}^*\left(\boldsymbol{V}^*\right)=\boldsymbol{V}^*$. So,
$$

\boldsymbol{B}^{G\left(\boldsymbol{V}^*\right)}\left(\boldsymbol{V}^*\right)=\boldsymbol{V}^*

$$
So $\boldsymbol{V}^*$ is the Fixed-Point of the Bellman Policy Operator $\boldsymbol{B}^{G\left(\boldsymbol{V}^*\right)}$ But we know $\boldsymbol{B}^{G\left(\boldsymbol{V}^*\right)}$ has a unique Fixed-Point $\left(=\boldsymbol{V}^{G\left(\boldsymbol{V}^*\right)}\right)$. So,
$$

\boldsymbol{V}^{G\left(\boldsymbol{V}^*\right)}=\boldsymbol{V}^*

$$
Evaluating MDP with greedy policy extracted from $\boldsymbol{V}^*$ achieves $\boldsymbol{V}^*$ So, $G\left(\boldsymbol{V}^*\right)$ is a (Deterministic) Optimal Policy  

### Value Function Progression in Policy Iteration

$$

\begin{gathered}

\pi_1=G\left(\boldsymbol{V}_{\mathbf{0}}\right): \boldsymbol{V}_{\mathbf{0}} \rightarrow \boldsymbol{B}^{\pi_1}\left(\boldsymbol{V}_{\mathbf{0}}\right) \rightarrow \ldots\left(\boldsymbol{B}^{\pi_1}\right)^i\left(\boldsymbol{V}_{\mathbf{0}}\right) \rightarrow \ldots \boldsymbol{V}^{\pi_1}=\boldsymbol{V}_{\mathbf{1}} \\

\pi_2=G\left(\boldsymbol{V}_{\mathbf{1}}\right): \boldsymbol{V}_{\mathbf{1}} \rightarrow \boldsymbol{B}^{\pi_2}\left(\boldsymbol{V}_{\mathbf{1}}\right) \rightarrow \ldots\left(\boldsymbol{B}^{\pi_2}\right)^i\left(\boldsymbol{V}_{\mathbf{1}}\right) \rightarrow \ldots \boldsymbol{V}^{\pi_2}=\boldsymbol{V}_{\mathbf{2}} \\

\ldots \\

\ldots \\

\pi_{j+1}=G\left(\boldsymbol{V}_{\boldsymbol{j}}\right): \boldsymbol{V}_{\boldsymbol{j}} \rightarrow \boldsymbol{B}^{\pi_{j+1}}\left(\boldsymbol{V}_{\boldsymbol{j}}\right) \rightarrow \ldots\left(\boldsymbol{B}^{\pi_{j+1}}\right)^i\left(\boldsymbol{V}_{\boldsymbol{j}}\right) \rightarrow \ldots \boldsymbol{V}^{\pi_{j+1}}=\boldsymbol{V}^*

\end{gathered}

$$

Policy Evaluation and Policy Improvement alternate until convergence, in the process competing to try and be consistent.  

### Generalised Policy Iteration Algorithm
#### Value Iteration and RL as GPI
Value Iteration takes only one step of Policy Evaluation.
$$

\begin{gathered}

\pi_1=G\left(\mathbf{V}_{\mathbf{0}}\right): \mathbf{V}_{\mathbf{0}} \rightarrow \boldsymbol{B}^{\pi_1}\left(\mathbf{V}_{\mathbf{0}}\right)=\mathbf{V}_{\mathbf{1}} \\

\pi_2=G\left(\mathbf{V}_{\mathbf{1}}\right): \mathbf{V}_{\mathbf{1}} \rightarrow \boldsymbol{B}^{\pi_2}\left(\mathbf{V}_{\mathbf{1}}\right)=\mathbf{V}_{\mathbf{2}} \\

\cdots \\

\cdots \\

\pi_{j+1}=G\left(\boldsymbol{V}_{\boldsymbol{j}}\right): \boldsymbol{V}_{\boldsymbol{j}} \rightarrow \boldsymbol{B}^{\pi_{j+1}}\left(\mathbf{V}_{\boldsymbol{j}}\right)=\mathbf{V}^*

\end{gathered}

$$
RL updates either a subset of states or just one state at a time. These can be thought of as partial Policy Evaluation/Improvement.
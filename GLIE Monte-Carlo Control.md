#ReinforcementLearning 
[[RL for Control]]

We can utilise the [[Monte-Carlo]] for control problems using [[Generalised Policy Iteration Algorithm]] as follows:
- Do Policy Evaluation with the Q-value function with Q-Value updates at the end of each episode.
- Do Policy Improvement with an $\epsilon$-greedy Policy (obtained from the Q-Value function estimate at any time step for any episode).

### Greedy in the Limit with Infinite Exploration (GLIE)
This is the behaviour satisfying the two properties:
1. All state-action pairs are explored infinitely many times, i.e., for all $s \in \mathcal{N}$, for all $a \in \mathcal{A}$, and $\operatorname{Count}_k(s, a)$ denoting the number of occurrences of $(s, a)$ pairs after $k$ episodes:
$$
\lim _{k \rightarrow \infty} \operatorname{Count}_k(s, a)=\infty
$$
2. The policy converges to a greedy policy, i.e., for all $s \in \mathcal{N}$, for all $a \in \mathcal{A}$, and $\pi_k(s, a)$ denoting the $\epsilon$-greedy policy obtained from the $Q$-Value Function estimate after $k$ episodes:
$$
\lim _b \pi_k(s, a)=\mathbb{I}_{a=\arg \max _{b \in \mathcal{A}} Q(s, b)}
$$

#### Algorithm
We then have the below procedure for each terminating trace experience (episode):
- Generate the trace experience (episode) with actions sampled from the $\epsilon$-greedy policy $\pi$ obtained from the estimate of the Q-Value Function that is available at the start of the trace experience. Also, sample the first state of the trace experience from a uniform distribution of states in $\mathcal{N}$. This ensures infinite exploration of both states and actions. Let's denote the contents of this trace experience as: $$
S_0, A_0, R_1, S_1, A_1, \ldots, R_T, S_T
$$ and define the trace experience return $G_t$ associated with $\left(S_t, A_t\right)$ as: $$
G_t=\sum_{i=t+1}^T \gamma^{i-t-1} \cdot R_i=R_{t+1}+\gamma \cdot R_{t+2}+\gamma^2 \cdot R_{t+3}+\ldots \gamma^{T-t-1} \cdot R_T
$$
- For each state $S_t$ and action $A_t$ in the trace experience, perform the following updates at the end of the trace experience:
$$
\begin{gathered}
\operatorname{Count}\left(S_t, A_t\right) \leftarrow \operatorname{Count}\left(S_t, A_t\right)+1 \\
Q\left(S_t, A_t\right) \leftarrow Q\left(S_t, A_t\right)+\frac{1}{\operatorname{Count}\left(S_t, A_t\right)} \cdot\left(G_t-Q\left(S_t, A_t\right)\right)
\end{gathered}
$$
- Let's say this trace experience is the $k$-th trace experience in the sequence of trace experiences. Then, at the end of the trace experience, set:
$$
\epsilon \leftarrow \frac{1}{k}
$$

It can also then be proved that the above-described GLIE Tabular Monte-Carlo Control algorithm converges to the Optimal Action-Value function: $Q(s, a) \rightarrow Q^*(s, a)$ for all $s \in \mathcal{N}$, for all $a \in \mathcal{A}$. Hence, GLIE Tabular Monte-Carlo Control converges to an Optimal (Deterministic) Policy $\pi^*$.

To extend this from the tabular to the function approximation formulation we have the update as:
$$
\Delta \boldsymbol{w}=\alpha \cdot\left(G_t-Q\left(S_t, A_t ; \boldsymbol{w}\right)\right) \cdot \nabla_{\boldsymbol{w}} Q\left(S_t, A_t ; \boldsymbol{w}\right)
$$



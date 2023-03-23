#ReinforcementLearning 
Abbreviated to LSPI. 

This is an [[Off-Policy Control]] algorithm based on [[Least-Squares RL Prediction]] (TD version). 
This is a utilisation of the [[Generalised Policy Iteration Algorithm]] as in [[GPI with Evaluation as Monte-Carlo]]:
1. Policy Evaluation as Least-Squares $Q$-Value Prediction. Specifically, the $Q$-Value for a policy $\pi$ is approximated as: $$
Q^\pi(s, a) \approx Q(s, a ; \boldsymbol{w})=\phi(s, a)^T \cdot \boldsymbol{w} \text { for all } s \in \mathcal{N}, \text { for all } a \in \mathcal{A}
$$with a direct linear-algebraic solve for the linear [[Function Approximation]] weights $w$ using batch experiences data generated using policy $\pi$.
2. $\epsilon$-Greedy Policy Improvement.

The basic idea of LSPI is that it does Generalised Policy Iteration (GPI) in the form of [[Q-Learning with Experience Replay]], with the key being that instead of doing the usual Q-Learning update after each atomic experience, we do [[Batch RL]] [[Q-Learning]] for the Policy Evaluation phase of GPI.

In LSPI, each iteration of GPI involves access to:
- The experiences data set $\mathcal{D}$.
- A Deterministic Target Policy (call it $\pi_D$ ), that is made available from the previous iteration of GPI.

Given $\mathcal{D}$ and $\pi_D$, the goal of each iteration of GPI is to solve for weights $w^*$ that minimises:
$$
\begin{aligned}
\mathcal{L}(\boldsymbol{w}) & =\sum_{i=1}^n\left(Q\left(s_i, a_i ; \boldsymbol{w}\right)-\left(r_i+\gamma \cdot Q\left(s_i^{\prime}, \pi_D\left(s_i^{\prime}\right) ; \boldsymbol{w}\right)\right)\right)^2 \\
& =\sum_{i=1}^n\left(\boldsymbol{\phi}\left(s_i, a_i\right)^T \cdot \boldsymbol{w}-\left(r_i+\gamma \cdot \boldsymbol{\phi}\left(s_i^{\prime}, \pi_D\left(s_i^{\prime}\right)\right)^T \cdot \boldsymbol{w}\right)\right)^2
\end{aligned}
$$
The solution for the weights $\boldsymbol{w}^*$ is attained by setting the semi-gradient of $\mathcal{L}(\boldsymbol{w})$ to 0 , i.e.,
$$
\sum_{i=1}^n \phi\left(s_i, a_i\right) \cdot\left(\boldsymbol{\phi}\left(s_i, a_i\right)^T \cdot \boldsymbol{w}^*-\left(r_i+\gamma \cdot \boldsymbol{\phi}\left(s_i^{\prime}, \pi_D\left(s_i^{\prime}\right)\right)^T \cdot \boldsymbol{w}^*\right)\right)=0
$$
We can calculate the solution $\boldsymbol{w}^*$ as $\boldsymbol{A}^{-1} \cdot \boldsymbol{b}$, where the $m \times m$ Matrix $\boldsymbol{A}$ is accumulated for each Transition step $\left(s_i, a_i, r_i, s_i^{\prime}\right)$ as:
$$
\boldsymbol{A} \leftarrow \boldsymbol{A}+\boldsymbol{\phi}\left(s_i, a_i\right) \cdot\left(\boldsymbol{\phi}\left(s_i, a_i\right)-\gamma \cdot \boldsymbol{\phi}\left(s_i^{\prime}, \pi_D\left(s_i^{\prime}\right)\right)\right)^T
$$
and the $m$-Vector $\boldsymbol{b}$ is accumulated at each atomic experience $\left(s_i, a_i, r_i, s_i^{\prime}\right)$ as:
$$
\boldsymbol{b} \leftarrow \boldsymbol{b}+\boldsymbol{\phi}\left(s_i, a_i\right) \cdot r_i
$$
With Sherman-Morrison incremental inverse, we can reduce the computational complexity from $O\left(m^3\right)$ to $O\left(m^2\right)$.
This solved $w^*$ defines an updated $Q$-Value Function as follows:
$$
Q\left(s, a ; \boldsymbol{w}^*\right)=\boldsymbol{\phi}(s, a)^T \cdot \boldsymbol{w}^*=\sum_{j=1}^m \phi_j(s, a) \cdot w_j^*
$$
This defines an updated, improved deterministic policy $\pi_D^{\prime}$ (serving as the Deterministic Target Policy for the next iteration of GPI):
$$
\pi_D^{\prime}(s)=\underset{a}{\arg \max } Q\left(s, a ; \boldsymbol{w}^*\right) \text { for all } s \in \mathcal{N}
$$
This least-squares solution of $\boldsymbol{w}^*$ (Prediction) is known as Least-Squares Temporal Difference for Q-Value, abbreviated as LSTDQ. Thus, LSPI is GPI with LSTDQ and greedy policy improvements. Note how LSTDQ in each iteration re-uses the same data $\mathcal{D}$, i.e., LSPI does experience-replay.
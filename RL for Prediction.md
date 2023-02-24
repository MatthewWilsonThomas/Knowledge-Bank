#ReinforcementLearning 

Prediction is the problem of estimating the Value Function of a [[Markov Decision Process]] (MDP) for a given policy $\pi$. This is equivalent to estimating the Value Function of the $\pi$-implied [[Markov Reward Process]] (MRP). Thus we can work with MRP theory. 

### Prediction Problem
Given a stream of atomic experiences or a stream of trace experiences, the RL Prediction problem is to estimate the Value Function $V: \mathcal{N} \rightarrow \mathbb{R}$ of the MRP defined as:
$$
V(s)=\mathbb{E}\left[G_t \mid S_t=s\right] \text { for all } s \in \mathcal{N}, \text { for all } t=0,1,2, \ldots
$$
where the Return $G_t$ for each $t=0,1,2, \ldots$ is defined as:
$$
G_t=\sum_{i=t+1}^{\infty} \gamma^{i-t-1} \cdot R_i=R_{t+1}+\gamma \cdot R_{t+2}+\gamma^2 \cdot R_{t+3}+\ldots=R_{t+1}+\gamma \cdot G_{t+1}
$$

### Relative Algorithms
As an overview of the various algorithms utilised in RL for Prediction we can see their relation with regards to the height and width of the backup space.
![[Screenshot 2023-02-22 at 9.48.55 AM.png]]
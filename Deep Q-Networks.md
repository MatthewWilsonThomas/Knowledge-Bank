#ReinforcementLearning 

(DQN)

This is an algorithm based of [[Q-Learning with Experience Replay]], reaping the benefits of [[Experience Replay]] for [[Q-Learning]] with a [[Deep Neural Network]] (Q-network) approximating the Q-Value function, there is also a second DNN (target network). 

The parameters $\boldsymbol{w}^{-}$of the target network are infrequently updated to be made equal to the parameters $\boldsymbol{w}$ of the Q-network. The purpose of the Q-network is to evaluate the Q-Value of the current state $s$ and the purpose of the target network is to evaluate the Q-Value of the next state $s^{\prime}$, which in turn is used to obtain the Q-Learning target (note that the Q-Value of the current state is $Q(s, a ; \boldsymbol{w})$ and the $\mathrm{Q}$ Learning target is $r+\gamma \cdot \max _{a^{\prime}} Q\left(s^{\prime}, a^{\prime} ; \boldsymbol{w}^{-}\right)$for a given atomic experience $\left.\left(s, a, r, s^{\prime}\right)\right)$.

[[Deep Learning]] is premised on the fact that the supervised learning targets (response values $y$ corresponding to predictor values $x$ ) are pre-generated fixed values. This is not the case in TD learning where the targets are dependent on the $Q$-Values. As $Q$-Values are updated at each step, the targets also get updated, and this correlation between the current state's Q-Value estimate and the target value typically leads to oscillations or divergence of the $Q$-Value estimate. By infrequently updating the parameters $w^{-}$of the target network (providing the target values) to be made equal to the parameters $w$ of the Q-network (which are updated at each iteration), the targets in the Q-Learning update are essentially kept fixed. This goes a long way in resolving the core issue of correlation between the current state's $Q$-Value estimate and the target values, helping considerably with convergence of the $Q$-Learning algorithm. Thus, $D Q N$ reaps the benefits of not just Experience-Replay in Q-Learning (which we articulated earlier), but also the benefits of having "fixed" targets. DNN utilises a parameter $C$ such that the updating of $\boldsymbol{w}^{-}$to be made equal to $w$ is done once every $C$ updates to $w$ (updates to $w$ are based on the usual Q-Learning update equation).

### Algorithm
At each time $t$ for each episode:
- Given state $S_t$, take action $A_t$ according to $\epsilon$-greedy policy extracted from Q-network values $Q\left(S_t, a ; \boldsymbol{w}\right)$.
- Given state $S_t$ and action $A_t$, obtain reward $R_{t+1}$ and next state $S_{t+1}$ from the environment.
- Append atomic experience $\left(S_t, A_t, R_{t+1}, S_{t+1}\right)$ in experience-replay memory $\mathcal{D}$.
- Sample a random mini-batch of atomic experiences $\left(s_i, a_i, r_i, s_i^{\prime}\right) \sim \mathcal{D}$.
- Using this mini-batch of atomic experiences, update the Q-network parameters $\boldsymbol{w}$ with the Q-learning targets based on "frozen" parameters $w^{-}$of the target network. $$
\Delta \boldsymbol{w}=\alpha \cdot \sum_i\left(r_i+\gamma \cdot \max _{a_i^{\prime}} Q\left(s_i^{\prime}, a_i^{\prime} ; \boldsymbol{w}^{-}\right)-Q\left(s_i, a_i ; \boldsymbol{w}\right)\right) \cdot \nabla_{\boldsymbol{w}} Q\left(s_i, a_i ; \boldsymbol{w}\right)
$$ $S_t \leftarrow S_{t+1}$
- Once every $C$ time steps, set $\boldsymbol{w}^{-} \leftarrow \boldsymbol{w}$.

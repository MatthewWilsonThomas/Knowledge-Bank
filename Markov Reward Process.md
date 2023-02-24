#Mathematics 
#StochasticMethods
#ReinforcementLearning

### Markov Reward Process
A Markov Reward Process is a [[Markov Process]], along with a time-indexed sequence of Reward random variables $R_t \in \mathcal{D}$ (a countable subset of $\mathbb{R}$) for time steps $t = 1, 2, ...$ satisfying the Markov Property (including Rewards): $\mathbb{P}[(R_{t+1}, S_{t+1})|S_t, S_{t-1}, ..., S_0] = \mathbb{P}[(R_{t+1}, S_{t+1})|S_t]$ for all $t \geq 0$.

The reward transition function $\mathcal{R}_T: \mathcal{N} \times \mathcal{S} \rightarrow \mathbb{R}$ is defined as:

$$

\mathcal{R}_T\left(s, s^{\prime}\right)=\mathbb{E}\left[R_{t+1} \mid S_{t+1}=s^{\prime}, S_t=s\right]

$$

$$

=\sum_{r \in \mathcal{D}} \frac{\mathcal{P}_R\left(s, r, s^{\prime}\right)}{\mathcal{P}\left(s, s^{\prime}\right)} \cdot r=\sum_{r \in \mathcal{D}} \frac{\mathcal{P}_R\left(s, r, s^{\prime}\right)}{\sum_{r \in \mathcal{D}} \mathcal{P}_R\left(s, r, s^{\prime}\right)} \cdot r

$$

The reward function $\mathcal{R}: \mathcal{N}\rightarrow\mathbb{R}$ is defined as:

$$

\mathcal{R}(s)=\mathbb{E}\left[R_{t+1} \mid S_t=s\right]

$$$$
=\sum_{s^{\prime} \in \mathcal{S}} \mathcal{P}\left(s, s^{\prime}\right) \cdot \mathcal{R}_T\left(s, s^{\prime}\right)=\sum_{s^{\prime} \in \mathcal{S}} \sum_{r \in \mathcal{D}} \mathcal{P}_R\left(s, r, s^{\prime}\right) \cdot r
$$

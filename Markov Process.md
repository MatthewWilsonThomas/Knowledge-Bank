#Mathematics 
#StochasticMethods
#ReinforcementLearning

### Markov Process
An Markov Process comprises of:
- A countable set of States $\mathcal{S}$ (State Space) and a set $\mathcal{T}\subseteq \mathcal{S}$ (Terminal States)
- A time-indexed sequence of random states $S_t \in \mathcal{S}$ for time sets $t = 0, 1, 2,...$ with each state transition satisfying the Markov Property: $\mathbb{P} [S_{t+1}| S_t, S_{t-1}, ..., S_0] = \mathbb{P}[S_{t+1}|S_t]$ for all $t \geq 0$
- Termination: If an outcome for $S_T$ (for some time step $T$) is a state in the set $\mathcal{T}$, the this sequence outcome terminates at time step $T$.

### Stationary Distribution
The stationary distribution of a (Time-Homogenous) Markov Process with state space $\mathcal{S} = \mathcal{N}$ and a transition probability function $\mathcal{P} : \mathcal{N}\times\mathcal{N}\rightarrow[0, 1]$ is a probability distribution function $\pi:\mathcal{N}\rightarrow[0,1]$ such that:
$$

\pi(s) = \sum_{s'\in\mathcal{N}}\pi(s)\cdot \mathcal{P}(s, s') \text{ for all } s \in \mathcal{N}

$$
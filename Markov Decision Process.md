#Mathematics 
#StochasticMethods
#ReinforcementLearning

A variant of a [[Markov Process]]

### Markov Decision Process
- A countable set of states $\mathcal{S}$ (state space), a set $\mathcal{T} \subseteq \mathcal{S}$ (terminal states), and a countable set of actions $\mathcal{A}$.
- A time-indexed sequence of envrionment-generated pairs of random states St∈S and random rewards Rt∈D (a countable subset of R) alternating with agent-controlled actions At∈A for time steps t=0,1,2,....
- Markov Property: $$P[(R_{t+1}, S_{t+1})|(S_t, A_t, S_{t-1}, A_{t-1})] = P[(R_{t+1}, S_{t+1})| (S_t, A_t)]\quad \forall t\geq0$$

If the process is time-homogeneous this process implies the transition probability function $\mathcal{P}_R: \mathcal{N}\times\mathcal{A}\times\mathcal{D}\times\mathcal{S}\rightarrow[0, 1]$:

$$

\mathcal{P}_R\left(s, a, r, s'\right)=\mathbb{P}\left[\left(R_{t+1}=r, S_{t+1}=s'\right) \mid S_t=s, A_t=a\right]

$$

There are also the following variations:
- State Transition Probability Function $\mathcal{P}_R: \mathcal{N}\times\mathcal{A}\times\mathcal{S}\rightarrow[0, 1]$:

$$

\mathcal{P}\left(s, a, s'\right)=\sum_{r \in \mathcal{D}} \mathcal{P}_R\left(s, a, r, s'\right)

$$
- Reward Transition Function $\mathcal{P}_R: \mathcal{N}\times\mathcal{A}\times\mathcal{S}\rightarrow\mathbb{R}$:

$$

\begin{aligned}

& \mathcal{R}_T\left(s, a, s'\right)=\mathbb{E}\left[R_{t+1} \mid\left(S_{t+1}=s', S_t=s, A_t=a\right)\right] \\

= & \sum_{r \in \mathcal{D}} \frac{\mathcal{P}_R\left(s, a, r, s'\right)}{\mathcal{P}\left(s, a, s'\right)} \cdot r=\sum_{r \in \mathcal{D}} \frac{\mathcal{P}_R\left(s, a, r, s'\right)}{\sum_{r \in \mathcal{D}} \mathcal{P}_R\left(s, a, r, s'\right)} \cdot r

\end{aligned}

$$
- Reward Function PR:N×A→R:

$$

\mathcal{R}(s, a)=\mathbb{E}\left[R_{t+1} \mid\left(S_t=s, A_t=a\right)\right]=\sum_{s' \in \mathcal{S}} \sum_{r \in \mathcal{D}} \mathcal{P}_R\left(s, a, r, s'\right) \cdot r

$$
### Policy
A policy is an Agent-Controlled function $\pi:\mathcal{N}\times\mathcal{A}\rightarrow[0, 1]$:

$$

\pi(s, a) = P[A_t = a|S_t = s] \quad \forall t = 0, 1, 2, ...

$$

(assuming that the policy is Markovian and Stationary)

### Finite MDP
In the finite case the state space is finite, and the action space for each state is also finite. This means we can have the currying of the state spaces giving the mapping $\mathcal{P}_R: \mathcal{N}\times\mathcal{A}\times\mathcal{D}\times\mathcal{S}\rightarrow[0, 1]$ as:

$$

\mathcal{P}_R: \mathcal{N}\rightarrow(\mathcal{A}\rightarrow(\mathcal{S}\times\mathcal{D}\rightarrow[0, 1]))

$$

### State-Value Function of MDP with a Fixed Policy
We define the Return $G_t$ from state $S_t$ as:

$$

G_t=\sum_{i=t+1}^{\infty} \gamma^{i-t-1} \cdot R_i=R_{t+1}+\gamma \cdot R_{t+2}+\gamma^2 \cdot R_{t+3}+\ldots

$$
$\gamma\in[0,1]$ is the discount factor.

We then have the State-Value Function (for the policy $\pi$) $\mathsf{V}^\pi:\mathcal{N}\rightarrow\mathbb{R}$ defined as:

$$

V^\pi(s)=\mathbb{E}_{\pi, \mathcal{P}_R}\left[G_t \mid S_t=s\right] \text { for all } s \in \mathcal{N}, \text { for all } t=0,1,2, \ldots

$$

Here $\mathsf{V}^\pi$ is the Value Function of the $\pi$ implied [[Markov Reward Process]], satisfying the MRP Bellman Equation:

$$

V^\pi(s)=\mathcal{R}^\pi(s)+\gamma \cdot \sum_{s' \in \mathcal{N}} \mathcal{P}^\pi\left(s, s'\right) \cdot V^\pi\left(s'\right)

$$

which yields the MDP (State-Value Function) Bellman Policy Equation:

$$

V^\pi(s)=\sum_{a \in \mathcal{A}} \pi(s, a) \cdot\left(\mathcal{R}(s, a)+\gamma \cdot \sum_{s' \in \mathcal{N}} \mathcal{P}\left(s, a, s'\right) \cdot V^\pi\left(s'\right)\right)

$$

### Action-Value Function of MDP with a Fixed Policy
Action-Value Function (for policy $\pi$ ) $Q^\pi: \mathcal{N} \times \mathcal{A} \rightarrow \mathbb{R}$ defined as:

$$

Q^\pi(s, a)=\mathbb{E}_{\pi, \mathcal{P}_R}\left[G_t \mid\left(S_t=s, A_t=a\right)\right] \text { for all } s \in \mathcal{N}, a \in \mathcal{A}

$$

$$

V^\pi(s)=\sum_{a \in \mathcal{A}} \pi(s, a) \cdot Q^\pi(s, a)

$$
Combining Equation (1) and Equation (2) yields:
$$

Q^\pi(s, a)=\mathcal{R}(s, a)+\gamma \cdot \sum_{s' \in \mathcal{N}} \mathcal{P}\left(s, a, s'\right) \cdot V^\pi\left(s'\right)

$$
Combining Equation (3) and Equation (2) yields:
$$

Q^\pi(s, a)=\mathcal{R}(s, a)+\gamma \cdot \sum_{s' \in \mathcal{N}} \mathcal{P}\left(s, a, s'\right) \sum_{a' \in \mathcal{A}} \pi\left(s', a'\right) \cdot Q^\pi\left(s', a'\right)

$$

## Optimal Value Functions
The optimal State-Value Function $\mathsf{V}^*: \mathcal{N} \rightarrow\mathbb{R}$ is defined as:

$$

V^*(s)=\max _{\pi \in \sqcap } V^\pi(s) \text { for all } s \in \mathcal{N}

$$

where $\sqcap$ is the space of all stationary (stochasitc) policies.

The optimal Action-Value function is equivalently $Q^*:\mathcal{N}\times\mathcal{A}\rightarrow\mathbb{R}$ defined as:
$$

Q^*(s, a)=\max _{\pi \in \sqcap} Q^\pi(s, a) \text { for all } s \in \mathcal{N}, a \in \mathcal{A}

$$  
### Bellman Optimality Equations

$$

V^*(s)=\max _{a \in \mathcal{A}} Q^*(s, a)

$$

$$

Q^*(s, a)=\mathcal{R}(s, a)+\gamma \cdot \sum_{s' \in \mathcal{N}} \mathcal{P}\left(s, a, s'\right) \cdot V^*\left(s'\right)

$$
These yield the MDP State-Value Bellman Optimality Equation
$$

V^*(s)=\max _{a \in \mathcal{A}}\left\{\mathcal{R}(s, a)+\gamma \cdot \sum_{s' \in \mathcal{N}} \mathcal{P}\left(s, a, s'\right) \cdot V^*\left(s'\right)\right\}

$$
and the MDP Action-Value Bellman Optimality Equation
$$

Q^*(s, a)=\mathcal{R}(s, a)+\gamma \cdot \sum_{s' \in \mathcal{N}} \mathcal{P}\left(s, a, s'\right) \cdot \max _{a' \in \mathcal{A}} Q^*\left(s', a'\right)

$$

### Partially-Observable MDP (POMDP)
In a POMDP there are two notions of state:
- Internal representation or the envrinment at each step $t$, $S_t^e$
- The agents state at each step t, $t$, $S_t^a$

When the MDP is fully observable we have $S_t^e = S_t^a = S_t$ and that $S_t$ is fully observable.
In the POMDP case the agent cannot see $S_t^e$ from the history of his Observations $O_t$.
The POMDP is specified with the Observation Space $\mathcal{O}$, implying the observation probability function $\mathcal{Z}:\mathcal{S}\times\mathcal{A}\times\mathcal{O}\rightarrow[0, 1]$:
$$

\mathcal{Z}\left(s', a, o\right)=\mathbb{P}\left[O_{t+1}=o \mid\left(S_{t+1}=s^{\prime}, A_t=a\right)\right]

$$
along with the usual transition probabilites in $\mathcal{P}_R$.

Since the Agent doesn't have knowledge of $S_t$ it must guess at the state by maintaining belief states:
$$
b(h)_t = (P[S_t = s_1|H_t = h], P[S_t = s_2|H_t = h],...)
$$
with the history $H_t$ is all the data known by the agent.

$H_t$ satisfies the Markov Property and therefore $b(h)_t$ satisfies the Markov Property. POMDPs yield huge MDP whose states are POMDPs belief states.
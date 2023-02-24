#Algorithm 
#ReinforcementLearning 
#Planning

This is a [[Dynamic Programming]] algorithm used for [[Markov Decision Process]] optimization.
We want to iterate policy improvements to drive an optimal policy. We use a greedy policy to do this.

### Greedy Policy
$\mathcal{G}:\mathbb{R}^m\rightarrow(\mathcal{N}\rightarrow\mathcal{A})$:
$$

G(\boldsymbol{V})(s)=\pi_D^{\prime}(s)=\underset{a \in \mathcal{A}}{\arg \max }\left\{\mathcal{R}(s, a)+\gamma \sum_{s^{\prime} \in \mathcal{N}} \mathcal{P}\left(s, a, s^{\prime}\right) \cdot \boldsymbol{V}\left(s^{\prime}\right)\right\}

$$We say $X \geq Y$ for Value Functions $X, Y: \mathcal{N} \rightarrow \mathbb{R}$ of an MDP iff:
$$

X(s) \geq Y(s) \text { for all } s \in \mathcal{N}

$$  

### Policy Improvement Theorem
For a finite MDP, for any policy $\pi$:

$$

\boldsymbol{V}^{\pi_D^{\prime}}=\boldsymbol{V}^{G\left(\boldsymbol{V}^\pi\right)} \geq \boldsymbol{V}^\pi

$$This can be proved by induction using the monotonicity property of the $\boldsymbol{B}^\pi$ operator.

This gives us a non-decreasing tower of Value Functions, where each state of further application of $\boldsymbol{B}^{\pi'_D}$ improves the Value Function.

Policy Improvment Theorem says:
- Start with Value Function $V^\pi$ (for policy $\pi$)
- Perform a greedy policy improvement to create policy $\pi_D^′=G(V^\pi)$
- Perform Policy Evaluation (for policy  $\pi_D^′$) with starting VF $V^\pi$
- Resulting in VF $V^{\pi'_D} \geq V^\pi$.
We can repeat this process, creating an improved policy stack, until we see no further improvment. This is the Policy Iteration Algorithm.

Starting with any Value Function $V_0\in\mathbb{R}^m$, iterating over $j = 0, 1, 2, ...$ we calculate (for each iterations):

The Deterministic Policy:
$$ \pi_{j+1} = G(V_j)$$
The Value Function:
$$ V_{j+1} = \lim_{i\rightarrow\infty}(B^{\pi_{j+1}})^i(V_j)$$
Then stop when:
$$ d(V_j, V_{j+1}) = \max_{x\in\mathcal{N}}|(V_j - V_{j+1})(s)| \leq \epsilon$$
Looking at $i = 1$, we have:
$$

\boldsymbol{V}_{\boldsymbol{j}}(s)=\boldsymbol{B}^{G\left(\boldsymbol{V}_{\boldsymbol{j}}\right)}\left(\boldsymbol{V}_{\boldsymbol{j}}\right)(s)=\max _{a \in \mathcal{A}}\left\{\mathcal{R}(s, a)+\gamma \sum_{s^{\prime} \in \mathcal{N}} \mathcal{P}\left(s, a, s^{\prime}\right) \cdot \boldsymbol{V}_{\boldsymbol{j}}\left(s^{\prime}\right)\right\}

$$
We can use the Policy Iteration Convergence Theorem to study the convergence of this value function, giving us the running times as:
- Runtime of Policy Improvement is $O(m^2k)$, where $|\mathcal{N}| = m, |\mathcal{A}| = k$
- Runtime of each iteration of Policy Evaluation if $O(m^2k)$.

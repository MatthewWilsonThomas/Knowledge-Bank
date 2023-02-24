#Algorithm 
#ReinforcementLearning 
#Planning

This is a [[Dynamic Programming]] algorithm used for [[Markov Decision Process]] optimisation.

### Bellman Optimality Operator
We can tweak the definition of the Greedy Policy function (to use argmax) to get the Bellman Optimality Operator $B^*:\mathbb{R}^m\rightarrow\mathbb{R}^m$:
$$

\boldsymbol{B}^*(\boldsymbol{V})(s)=\max _{a \in \mathcal{A}}\left\{\mathcal{R}(s, a)+\gamma \sum_{s^{\prime} \in \mathcal{N}} \mathcal{P}\left(s, a, s^{\prime}\right) \cdot \boldsymbol{V}\left(s^{\prime}\right)\right\}

$$
This is a non-linear transformation of a VF vector. The action $a$ producing the max is that action prescribed by $G(V)$, so:
$$

\boldsymbol{B}^{G(\boldsymbol{V})}(\boldsymbol{V})=\boldsymbol{B}^*(\boldsymbol{V}) \text { for all } \boldsymbol{V} \in \mathbb{R}^m

$$
Specialising $V$ to be the value function $V^\pi$ gives:

$$

\boldsymbol{B}^{G\left(\boldsymbol{V}^\pi\right)}\left(\boldsymbol{V}^\pi\right)=\boldsymbol{B}^*\left(\boldsymbol{V}^\pi\right)

$$

### Fixed-Point of Bellman Optimality Operator
$B^*$ is motivated by the MDP Bellman Optimality Equation, giving $B^*$ as the Bellman Optimality Operator for:
$$

\boldsymbol{V}^*(s)=\max _{a \in \mathcal{A}}\left\{\mathcal{R}(s, a)+\gamma \sum_{s^{\prime} \in \mathcal{N}} \mathcal{P}\left(s, a, s^{\prime}\right) \cdot \boldsymbol{V}^*\left(s^{\prime}\right)\right\} \text { for all } s \in \mathcal{N}

$$
this means that $V^*$ is a fixed-point of $B^*$.

We can also prove that $B^*$ is a contraction using its monotonicity and its constant shift property.

### Value Iteration Algorithm
This gives the the Value Iteration Algorithm.
Start with any Value Function $V_0 \in \mathbb{R}^m$
Iterating over $i=0,1,2, \ldots$, calculate in each iteration:
$$

V_{i+1}(s)=B^*\left(V_i\right)(s) \text { for all } s \in \mathcal{N}

$$
Stop when $d\left(\boldsymbol{V}_{\boldsymbol{i}}, \boldsymbol{V}_{\boldsymbol{i}+\boldsymbol{1}}\right)=\max _{\boldsymbol{s} \in \mathcal{N}}\left|\left(\boldsymbol{V}_{\boldsymbol{i}}-\boldsymbol{V}_{\boldsymbol{i}+\boldsymbol{1}}\right)(s)\right|$ is small enough.
The running time of each iteration of Value Iteration is $O(m^2k)$ where $|\mathcal{N}| = m, |\mathcal{A}| = k$.
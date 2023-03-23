#ReinforcementLearning 
[[RL for Control]]

We can utilise the [[Monte-Carlo]] for control problems using [[Generalised Policy Iteration Algorithm]].
### $\epsilon$-greedy policy
For future reference we have the definition of the $\epsilon$-greedy stochastic policy $\pi'$ for a finite MDP:
$$
\text { Improved Stochastic Policy } \pi^{\prime}(s, a)= \begin{cases}\frac{\epsilon}{|\mathcal{A}|}+1-\epsilon & \text { if } a=\arg \max _{b \in \mathcal{A}} Q(s, b) \\ \frac{\epsilon}{|\mathcal{A}|} & \text { otherwise }\end{cases}
$$

To use an $\epsilon$-greedy policy in GPI we need to prove that it is an improved policy.
#### Proof
Theorem:
For a Finite $M D P$, if $\pi$ is a policy such that for all $s \in \mathcal{N}, \pi(s, a) \geq \frac{\epsilon}{|\mathcal{A}|}$ for all $a \in \mathcal{A}$, then the $\epsilon$-greedy policy $\pi^{\prime}$ obtained from $Q^\pi$ is an improvement over $\pi$, i.e., $\boldsymbol{V}^{\pi^{\prime}}(s) \geq$ $V^\pi(s)$ for all $s \in \mathcal{N}$.

Proof. We've previously learnt that for any policy $\pi^{\prime}$, if we apply the Bellman Policy Operator $\boldsymbol{B}^{\pi^{\prime}}$ repeatedly (starting with $\boldsymbol{V}^\pi$ ), we converge to $\boldsymbol{V}^{\pi^{\prime}}$. In other words,
$$
\lim _{i \rightarrow \infty}\left(\boldsymbol{B}^{\pi^{\prime}}\right)^i\left(\boldsymbol{V}^\pi\right)=\boldsymbol{V}^{\pi^{\prime}}
$$
So the proof is complete if we prove that:
$$
\left(\boldsymbol{B}^{\pi^{\prime}}\right)^{i+1}\left(\boldsymbol{V}^\pi\right) \geq\left(\boldsymbol{B}^{\pi^{\prime}}\right)^i\left(\boldsymbol{V}^\pi\right) \text { for all } i=0,1,2, \ldots
$$
In plain English, this says we need to prove that repeated application of $\boldsymbol{B}^{\pi^{\prime}}$ produces a non-decreasing sequence of Value Functions $\left[\left(\boldsymbol{B}^{\pi^{\prime}}\right)^i\left(\boldsymbol{V}^\pi\right) \mid i=0,1,2, \ldots\right]$. We prove this by induction. The base case of the proof by induction is to show that $\boldsymbol{B}^{\pi^{\prime}}\left(\boldsymbol{V}^\pi\right) \geq \boldsymbol{V}^\pi$
$$
\begin{aligned}
\boldsymbol{B}^{\pi^{\prime}}\left(\boldsymbol{V}^\pi\right)(s) & =\left(\mathcal{R}^{\pi^{\prime}}+\gamma \cdot \mathcal{P}^{\pi^{\prime}} \cdot \boldsymbol{V}^\pi\right)(s) \\
& =\mathcal{R}^{\pi^{\prime}}(s)+\gamma \cdot \sum_{s^{\prime} \in \mathcal{N}} \mathcal{P}^{\pi^{\prime}}\left(s, s^{\prime}\right) \cdot \boldsymbol{V}^\pi\left(s^{\prime}\right) \\
& =\sum_{a \in \mathcal{A}} \pi^{\prime}(s, a) \cdot\left(\mathcal{R}(s, a)+\gamma \cdot \sum_{s^{\prime} \in \mathcal{N}} \mathcal{P}\left(s, a, s^{\prime}\right) \cdot \boldsymbol{V}^\pi\left(s^{\prime}\right)\right) \\
& =\sum_{a \in \mathcal{A}} \pi^{\prime}(s, a) \cdot Q^\pi(s, a) \\
& =\sum_{a \in \mathcal{A}} \frac{\epsilon}{|\mathcal{A}|} \cdot Q^\pi(s, a)+(1-\epsilon) \cdot \max _{a \in \mathcal{A}} Q^\pi(s, a) \\
& \geq \sum_{a \in \mathcal{A}} \frac{\epsilon}{|\mathcal{A}|} \cdot Q^\pi(s, a)+(1-\epsilon) \cdot \sum_{a \in \mathcal{A}} \frac{\pi(s, a)-\frac{\epsilon}{|\mathcal{A}|}}{1-\epsilon} \cdot Q^\pi(s, a) \\
& =\sum_{a \in \mathcal{A}} \pi(s, a) \cdot Q^\pi(s, a) \\
& =\boldsymbol{V}^\pi(s) \text { for all } s \in \mathcal{N}
\end{aligned}
$$
The line with the inequality above is due to the fact that for any fixed $s \in \mathcal{N}$, $\max _{a \in \mathcal{A}} Q^\pi(s, a) \geq \sum_{a \in \mathcal{A}} w_a \cdot Q^\pi(s, a)$ (maximum Q-Value greater than or equal to a weighted average of all $Q$-Values, for a given state) with the weights $w_a=\frac{\pi(s, a)-\frac{\epsilon}{\mid} \mid}{1-\epsilon}$ such that $\sum_{a \in \mathcal{A}} w_a=1$ and $0 \leq w_a \leq 1$ for all $a \in \mathcal{A}$.
This completes the base case of the proof by induction.
The induction step is easy and is proved as a consequence of the monotonicity property of the $B^\pi$ operator (for any $\pi$ ), which is defined as follows:
Monotonicity Property of $\boldsymbol{B}^\pi: \boldsymbol{X} \geq \boldsymbol{Y} \Rightarrow \boldsymbol{B}^\pi(\boldsymbol{X}) \geq \boldsymbol{B}^\pi(\boldsymbol{Y})$
Note that we proved the monotonicity property of the $\boldsymbol{B}^\pi$ operator in Chapter 5. A straightforward application of this monotonicity property provides the induction step of the proof:
$$
\left(\boldsymbol{B}^{\pi^{\prime}}\right)^{i+1}\left(\boldsymbol{V}^\pi\right) \geq\left(\boldsymbol{B}^{\pi^{\prime}}\right)^i\left(\boldsymbol{V}^\pi\right) \Rightarrow\left(\boldsymbol{B}^{\pi^{\prime}}\right)^{i+2}\left(\boldsymbol{V}^\pi\right) \geq\left(\boldsymbol{B}^{\pi^{\prime}}\right)^{i+1}\left(\boldsymbol{V}^\pi\right) \text { for all } i=0,1,2, \ldots
$$
This completes the proof.


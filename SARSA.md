#ReinforcementLearning 
[[RL for Control]]

In this case we replace Monte-Carlo control with [[Temporal-Difference]] control as a biased estimate of $G_t$ when updating. This results in the new update:
$$
\Delta \boldsymbol{w}=\alpha \cdot\left(R_{t+1}+\gamma \cdot Q\left(S_{t+1}, A_{t+1} ; \boldsymbol{w}\right)-Q\left(S_t, A_t ; \boldsymbol{w}\right)\right) \cdot \nabla_{\boldsymbol{w}} Q\left(S_t, A_t ; \boldsymbol{w}\right)
$$
Similarly to standard TD we can update continuously, i.e. not only at the end of a trace experience. This gives us a Q-Value function update after each atomic experience. 

We can see in the above update equation the parameters:
- State $S_t$
- Action $A_t$
- Reward $R_t$
- State $S_{t+1}$
- Action $A_{t+1}$
Giving this algorithm its name (SARSA). 

Theorem:
Tabular SARSA converges to the Optimal Action-Value function, $Q(s, a) \rightarrow$ $Q^*(s, a)$ (hence, converges to an Optimal Deterministic Policy $\pi^*$ ), under the following conditions:
- GLIE schedule of policies $\pi_t(s, a)$
- Robbins-Monro schedule of step-sizes $\alpha_t$ :
$$
\begin{aligned}
& \sum_{t=1}^{\infty} \alpha_t=\infty \\
& \sum_{t=1}^{\infty} \alpha_t^2<\infty
\end{aligned}
$$
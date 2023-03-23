#ReinforcementLearning 
[[RL for Control]]

We can extend [[SARSA]] to SARSA($\lambda$) to give us a way to tune the spectrum from [[GLIE Monte-Carlo Control]] to [[SARSA]] using the $\lambda$ parameter.

### 2-step Bootstrapped SARSA
The update function for this variation is:
$$
\Delta \boldsymbol{w}=\alpha \cdot\left(R_{t+1}+\gamma \cdot R_{t+2}+\gamma^2 \cdot Q\left(S_{t+2}, A_{t+2} ; \boldsymbol{w}\right)-Q\left(S_t, A_t ; \boldsymbol{w}\right)\right) \cdot \nabla_{\boldsymbol{w}} Q\left(S_t, A_t ; \boldsymbol{w}\right)
$$

### n-step Bootstrapped SARSE
The update function for this variant is:
$$
\Delta \boldsymbol{w}=\alpha \cdot\left(G_{t, n}-Q\left(S_t, A_t ; \boldsymbol{w}\right)\right) \cdot \nabla_{\boldsymbol{w}} Q\left(S_t, A_t ; \boldsymbol{w}\right)
$$
where the $n$-step-bootstrapped Return $G_{t, n}$ is defined as:
$$
\begin{aligned}
G_{t, n} & =\sum_{i=t+1}^{t+n} \gamma^{i-t-1} \cdot R_i+\gamma^n \cdot Q\left(S_{t+n}, A_{t+n} ; \boldsymbol{w}\right) \\
& =R_{t+1}+\gamma \cdot R_{t+2}+\ldots+\gamma^{n-1} \cdot R_{t+n}+\gamma^n \cdot Q\left(S_{t+n}, A_{t+n} ; \boldsymbol{w}\right)
\end{aligned}
$$
Instead of $G_{t, n}$, a valid target is a weighted-average target:
$$
\sum_{n=1}^N u_n \cdot G_{t, n}+u \cdot G_t \text { where } u+\sum_{n=1}^N u_n=1
$$
Any of the $u_n$ or $u$ can be 0 , as long as they all sum up to 1 . The $\lambda$-Return target is a special case of weights $u_n$ and $u$, defined as follows:
$$
\begin{gathered}
u_n=(1-\lambda) \cdot \lambda^{n-1} \text { for all } n=1, \ldots, T-t-1 \\
u_n=0 \text { for all } n \geq T-t \text { and } u=\lambda^{T-t-1}
\end{gathered}
$$
We denote the $\lambda$-Return target as $G_t^{(\lambda)}$, defined as:
$$
G_t^{(\lambda)}=(1-\lambda) \cdot \sum_{n=1}^{T-t-1} \lambda^{n-1} \cdot G_{t, n}+\lambda^{T-t-1} \cdot G_t
$$
Then, the Offline $\lambda$-Return SARSA Algorithm makes the following updates (performed at the end of each trace experience) for each $\left(S_t, A_t\right)$ encountered in the trace experience:
$$
\Delta \boldsymbol{w}=\alpha \cdot\left(G_t^{(\lambda)}-Q\left(S_t, A_t ; \boldsymbol{w}\right)\right) \cdot \nabla_{\boldsymbol{w}} Q\left(S_t, A_t ; \boldsymbol{w}\right)
$$
Finally, we create the SARSA $(\lambda)$ Algorithm, which is the online "version" of the above $\lambda$-Return SARSA Algorithm. The calculations/updates at each time step $t$ for each trace experience are as follows:
$$
\begin{gathered}
\delta_t=R_{t+1}+\gamma \cdot Q\left(S_{t+1}, A_{t+1} ; \boldsymbol{w}\right)-Q\left(S_t, A_t ; \boldsymbol{w}\right) \\
\boldsymbol{E}_t=\gamma \lambda \cdot \boldsymbol{E}_{t-1}+\nabla_{\boldsymbol{w}} Q\left(S_t, A_t ; \boldsymbol{w}\right) \\
\Delta \boldsymbol{w}=\alpha \cdot \delta_t \cdot \boldsymbol{E}_t
\end{gathered}
$$
with the eligibility traces initialised at time 0 for each trace experience as $\boldsymbol{E}_0=\nabla_{\boldsymbol{w}} V\left(S_0 ; \boldsymbol{w}\right)$. Note that just like in SARSA, the $\epsilon$-greedy policy improvement is automatic from the updated Q-Value Function estimate after each time step.

#ReinforcementLearning 
[[TD(Lambda) Prediction]]

Eligibility traces are based of a Memory function $M$:
$$
M(t)= \begin{cases}\mathbb{I}_{t=t_1} & \text { if } t \leq t_1, \text { else } \\ M\left(t_i\right) \cdot \theta^{t-t_i}+\mathbb{I}_{t=t_{i+1}} & \text { if } t_i<t \leq t_{i+1} \text { for any } 1 \leq i<n, \text { else } \\ M\left(t_n\right) \cdot \theta^{t-t_n} & \text { otherwise (i.e., if } \left.t>t_n\right)\end{cases}
$$
i.e. the function $M$ produces a time-decaying count of the event occurrences. 

### Eligibility Traces
The Eligibility Trace for each state $s \in \mathcal{N}$ is defined as the Memory function $M(\cdot)$ with $\theta = \gamma\cdot\lambda$ (product of discount factor and the TD-$\lambda$ parameter). Thus, the eligibility traces for a given trace experience at any time step $t$ as a function $E_t: \mathcal{N} \rightarrow \mathbb{R}_{\geq 0}$ is:
$$
E_0(s)=\mathbb{I}_{S_0=s}, \text { for all } s \in \mathcal{N}
$$
$$E_t(s)=\gamma \cdot \lambda \cdot E_{t-1}(s)+\mathbb{I}_{S_t=s}, \text{ for all } s \in \mathcal{N}, \text{ for all } t=1,2, \ldots$$
Then the Tabular TD($\lambda$) Prediction algorithm performs the following update:
$$V(s) \leftarrow V(s)+\alpha \cdot\left(R_{t+1}+\gamma \cdot V\left(S_{t+1}\right)-V\left(S_t\right)\right) \cdot E_t(s), \text{ for all } s \in \mathcal{N}$$

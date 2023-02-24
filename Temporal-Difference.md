#ReinforcementLearning 

### For Prediction
We can utilise Temporal-Difference Prediction to solve the [[RL for Prediction]] problem. 
This algorithm performs supervised learning to predict the expected return from any state of a [[Markov Reward Process]] i.e. it estimate the Value Function of the MRP.  

### Tabular TD
We have the Value Function Update in Tabular [[Monte-Carlo]] ([[Tabular RL]]) Prediction with a constant learning rate as the starting point:
$$
V\left(S_t\right) \leftarrow V\left(S_t\right)+\alpha \cdot\left(G_t-V\left(S_t\right)\right)
$$
To move to TD from MC is to take advantage of the recursive nature of the MRP [[Bellman Equation]], this allows us to write the update for Tabular TD Prediction as:
$$
V\left(S_t\right) \leftarrow V\left(S_t\right)+\alpha \cdot\left(R_{t+1}+\gamma \cdot V\left(S_{t+1}\right)-V\left(S_t\right)\right)
$$
replacing $G_t$ in the above equation with $R_{t+1} + \gamma \cdot V(S_{t+1})$. 

The TD target is $R_{t+1}+\gamma \cdot V\left(S_{t+1}\right)$
The TD Error is $\delta_t=R_{t+1}+\gamma \cdot V\left(S_{t+1}\right)-V(S_t)$

The TD Error represents the sample Bellman Error and is used to move $V(S_t))$ appropriately, i.e. bridging the TD Error (on an expected basis). 

### Loss Function
We start with the MC Loss function for a single state, and do the same substitution as above (replacing $G_t$ in the above equation with $R_{t+1} + \gamma \cdot V(S_{t+1})$):
$$
\mathcal{L}_{\left(S_t, S_{t+1}, R_{t+1}\right)}(\boldsymbol{w})=\frac{1}{2} \cdot\left(V\left(S_t ; \boldsymbol{w}\right)-\left(R_{t+1}+\gamma \cdot V\left(S_{t+1} ; \boldsymbol{w}\right)\right)\right)^2
$$
In this case we cheat in calculating the gradient by ignoring the dependency of $V(s;w)$ on $w$, giving the semi-gradient parameter update as:
$$
\Delta \boldsymbol{w}=\alpha \cdot\left(R_{t+1}+\gamma \cdot V\left(S_{t+1} ; \boldsymbol{w}\right)-V\left(S_t ; \boldsymbol{w}\right)\right) \cdot \nabla_{\boldsymbol{w}} V\left(S_t ; \boldsymbol{w}\right)
$$
### Learning Rate
To effectively implement Tabular TD for Prediction we are required to have a learning rate scheduler which lowers the learning rate as a function of the number of occurrences of a state in the atomic experience stream, i.e:
$$
\alpha_n=\frac{\alpha}{1+\left(\frac{n-1}{H}\right)^\beta}
$$
### Convergence 
Tabular TD Prediction converges to the true value function in the mean for constant learning rate, and converges to the true value function if the following stochastic approximation conditions are satisfied for the learning rate schedule $\alpha_n, n=1,2, \ldots$, where the index $n$ refers to the $n$-th occurrence of a particular state whose Value Function is being updated:
$$
\sum_{n=1}^{\infty} \alpha_n=\infty \text { and } \sum_{n=1}^{\infty} \alpha_n^2<\infty
$$



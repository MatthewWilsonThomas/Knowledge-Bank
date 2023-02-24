#Mathematics 
#Simulation 
#BayesianAnalysis 
#ReinforcementLearning 

### For Prediction
We can utilise Monte-Carlo Prediction to solve the [[RL for Prediction]] problem. 
This algorithm performs supervised learning to predict the expected return from any state of a [[Markov Reward Process]] i.e. it estimate the Value Function of the MRP.  

### Loss Function
Assuming the probability distribution of returns conditional on state is modelled by a function approximation as a state-conditional normal distributions, whose mean (Value Function) is denoted as $V(s; w)$, $s$ is state and $w$ are weights of the function approximation. Then the loss function for supervised learning of the Value Function is the sum of squares of differences between the observed returns and the Value Function estimate from the function approximation. 
For a state $S_t$ visited at $t$ in a trace with an associated return of $G_t$ the contribution to the loss is:
$$
\mathcal{L}_{\left(S_t, G_t\right)}(\boldsymbol{w})=\frac{1}{2} \cdot\left(V\left(S_t ; \boldsymbol{w}\right)-G_t\right)^2
$$
Giving the gradient as:
$$
\nabla_{\boldsymbol{w}} \mathcal{L}_{\left(S_t, G_t\right)}(\boldsymbol{w})=\left(V\left(S_t ; \boldsymbol{w}\right)-G_t\right) \cdot \nabla_{\boldsymbol{w}} V\left(S_t ; \boldsymbol{w}\right)
$$
This gives the parameter update as (the negative gradient of the loss function scaled by the learning rate):
$$
\Delta \boldsymbol{w}=\alpha \cdot\left(G_t-V\left(S_t ; \boldsymbol{w}\right)\right) \cdot \nabla_{\boldsymbol{w}} V\left(S_t ; \boldsymbol{w}\right)
$$


### Tabular Monte-Carlo
When we have a simple case of Monte-Carlo Prediction where the MRP consists of a finite state space with the non-terminal states $\mathcal{N}=\left\{s_1, s_2, \ldots, s_m\right\}$. In this case the Value Function is in tabular form, i.e. a dictionary of (state, expected return) pairs. 

In this case Monte-Carlo Prediction reduces to maintaining an the average of the trace experience return from that state onwards, and updating the average in an incremental manner. 

We then have the incremental update of the Tabular MC ([[Tabular RL]]) as:
$$
V_n\left(s_i\right)=(1-f(n)) \cdot V_{n-1}\left(s_i\right)+f(n) \cdot Y_i^{(n)}=V_{n-1}\left(s_i\right)+f(n) \cdot\left(Y_i^{(n)}-V_{n-1}\left(s_i\right)\right)
$$
with the $f(n)$ function calculating the weighting associated with each sample.
With the default of $f(n) = \frac{1}{n}$ we get:
$$
V_n\left(s_i\right)=\frac{n-1}{n} \cdot V_{n-1}\left(s_i\right)+\frac{1}{n} \cdot Y_i^{(n)}=V_{n-1}\left(s_i\right)+\frac{1}{n} \cdot\left(Y_i^{(n)}-V_{n-1}\left(s_i\right)\right)
$$
Expanding this update across the value of $n$ gives:
$$
\begin{aligned}
V_n\left(s_i\right)= & f(n) \cdot Y_i^{(n)}+(1-f(n)) \cdot f(n-1) \cdot Y_i^{(n-1)}+\ldots \\
& +(1-f(n)) \cdot(1-f(n-1)) \cdots(1-f(2)) \cdot f(1) \cdot Y_i^{(1)}
\end{aligned}
$$
with the default $f(n)$ again giving:
$$
V_n\left(s_i\right)=\frac{1}{n} \cdot Y_i^{(n)}+\frac{n-1}{n} \cdot \frac{1}{n-1} \cdot Y_i^{(n-1)}+\ldots+\frac{n-1}{n} \cdot \frac{n-2}{n-1} \cdots \frac{1}{2} \cdot \frac{1}{1} \cdot Y_i^{(1)}=\frac{\sum_{k=1}^n Y_i^{(k)}}{n}
$$
To add an element of forgetfulness in this algorithm, we can set the $f(n) = \alpha < 1$ resulting in:
$$
\lim _{n \rightarrow \infty} \sum_{j=1}^n \alpha \cdot(1-\alpha)^{n-j}=\lim _{n \rightarrow \infty} 1-(1-\alpha)^n=1
$$

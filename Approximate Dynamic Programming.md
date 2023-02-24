#Algorithm 
#ReinforcementLearning 
#Planning 

[[Dynamic Programming]] Algorithms are meant for non-large finite spaces, the DP algorithms typically sweep through all states in each iteration. However, this cannot be done for large finite spaces or infinite spaces.  

Thus we are required to generalize this theory to function approximations of the Value Function.
We can:
- Sample an appropriate subset of states.
- Calculate the Value Function for the states (Bellman Calculation).
- Create/Update a function approximation with the samples states' calculated values.

### Function Approximation
We work with a generic but simple setting, we have a predictor variable $x\in\mathcal{X}$ and a response variable $y\in\mathbb{R}$.
We want to estimate a function approximation for $P[y|x]$ from the data. We will consider parameterized functions $f$ with parameters denoted $w$. We have the estimated probability of $y|x := f(x; w)(y)$.
The data is in the form of a sequence of $x, y$ pairs, with the formalisation of the estimation as solving for $w = w^*$:
$$

w^* = \arg\max_w \left\{\prod_{i=1}^n f(x_i;w)(y)\right\} = \arg\max_w \left\{\sum_{i=1}^n\log f(x_i;w)(y_i) \right\}

$$

### Maximum Likelihood and Cross Entorpy Loss
The data specifies the empirical probability distribution $D$.

The parameterized function $f$ specifies the model probability distribution $M$. We wish to match $M$ to $D$, i.e. minimze the cross-entropy between $D$ and $M$:
$$

\text{Cross-Entropy Loss:}\quad \mathcal{H}(D, M) = -E[\log M]_D

$$
We allow for incremental estimation, updating parameters with gradient descent. We allow for all types of graddesc (full, mini, SGD). With an estimate of $f(x; w)$ we can predict $y|x$ as $E[y|x]_M$:

$$

E[y|x]_M = E[y]_{f(x;w)} = \int_{-\infty}^{\infty} y\cdot f(x;w)(y)\cdot dy

$$
### Linear Functions
Define a sequence of feature functions $\phi_j: \mathcal{X} \rightarrow \mathbb{R}, j=1,2, \ldots, m$ Feature Vector $\phi(x)=\left(\phi_1(x), \phi_2(x), \ldots, \phi_m(x)\right)$ for all $x \in \mathcal{X}$.

Parameters $w$ is a weights vector $w=\left(w_1, w_2, \ldots, w_m\right) \in \mathbb{R}^m$
Linear function approximation assumes gaussian distribution for $y \mid x$
Ω
with mean $=\sum_{j=1}^m \phi_j(x) \cdot w_j=\phi(x)^T \cdot w$ and constant variance $\sigma^2$
$$

\mathbb{P}[y \mid x]=f(x ; w)(y)=\frac{1}{\sqrt{2 \pi \sigma^2}} \cdot e^{-\frac{\left(y-\phi(x)^T \cdot w\right)^2}{2 \sigma^2}}

$$
Regularized cross-entropy loss function for data $\left[x_i, y_i \mid 1 \leq i \leq n\right]$ :

$$

\mathcal{L}(w)=\frac{1}{2 n} \cdot \sum_{i=1}^n\left(\phi\left(x_i\right)^T \cdot w-y_i\right)^2+\frac{1}{2} \cdot \lambda \cdot|\boldsymbol{w}|^2

$$

This ignores constants involving $\sigma$, and $\lambda$ is regularization coefficient So $\mathcal{L}(w)$ is just MSE of linear predictions $\phi\left(x_i\right)^T \cdot w$.

With gradient descent this becomes, the Gradient of $\mathcal{L}(\boldsymbol{w})$ with respect to $\boldsymbol{w}$ works out to:

$$

\nabla_w \mathcal{L}(\boldsymbol{w})=\frac{1}{n} \cdot\left(\sum_{i=1}^n \phi\left(x_i\right) \cdot\left(\phi\left(x_i\right)^T \cdot \boldsymbol{w}-y_i\right)\right)+\lambda \cdot w

$$

Solve for $\boldsymbol{w}^*$ by incremental estimation using gradient descent Gradient estimate $\mathcal{G}_{\left(x_t, y_t\right)}\left(\boldsymbol{w}_t\right)$ for time $t$-data $\left[\left(x_{t, i}, y_{t, i}\right) \mid 1 \leq i \leq n_t\right]$ :
$$

\mathcal{G}_{\left(x_t, y_t\right)}\left(\boldsymbol{w}_t\right)=\frac{1}{n} \cdot\left(\sum_{i=1}^{n_t} \phi\left(x_{t, i}\right) \cdot\left(\phi\left(x_{t, i}\right)^T \cdot \boldsymbol{w}_t-y_{t, i}\right)\right)+\lambda \cdot \boldsymbol{w}_t

$$
Interpreted as the weighted-mean of the feature vectors $\phi\left(x_{t, i}\right)$ Weighted by the (scalar) linear prediction errors $\phi\left(x_{t, i}\right)^T \cdot \boldsymbol{w}_t-y_{t, i}$ So the update to the weights vector $w$ is given by:
$$

\boldsymbol{w}_{t+1}=\boldsymbol{w}_t-\alpha_t \cdot \mathcal{G}_{\left(x_t, y_t\right)}\left(\boldsymbol{w}_t\right)

$$We also have a direction solution to a Linear Function Approximation, if .i.e if the feature funcitons are not too large, we can directly solve for $w^*$.

Assume the entire provided data is $\left[\left(x_i, y_i\right) \mid 1 \leq i \leq n\right]$. Then the gradient estimate based can be set to 0 to solve for $\boldsymbol{w}^*$
$$

\frac{1}{n} \cdot\left(\sum_{i=1}^n \phi\left(x_i\right) \cdot\left(\phi\left(x_i\right)^T \cdot \boldsymbol{w}^*-y_i\right)\right)+\lambda \cdot \boldsymbol{w}^*=0

$$enote $\boldsymbol{\Phi}$ as $n \times m$ matrix: $\boldsymbol{\Phi}_{i, j}=\phi_j\left(x_i\right)$

Denote column vector $\boldsymbol{Y} \in \mathbb{R}^n$ defined as $\boldsymbol{Y}_i=y_i$
$$

\begin{gathered}

\frac{1}{n} \cdot \boldsymbol{\Phi}^T \cdot\left(\boldsymbol{\Phi} \cdot \boldsymbol{w}^*-\boldsymbol{Y}\right)+\lambda \cdot \boldsymbol{w}^*=0 \\

\Rightarrow\left(\boldsymbol{\Phi}^T \cdot \boldsymbol{\Phi}+n \lambda \cdot \boldsymbol{I}_{\boldsymbol{m}}\right) \cdot \boldsymbol{w}^*=\boldsymbol{\Phi}^T \cdot \boldsymbol{Y} \\

\Rightarrow \boldsymbol{w}^*=\left(\boldsymbol{\Phi}^T \cdot \boldsymbol{\Phi}+n \lambda \cdot \boldsymbol{I}_{\boldsymbol{m}}\right)^{-1} \cdot \boldsymbol{\Phi}^T \cdot \boldsymbol{Y}

\end{gathered}

$$

### Approximate Policy Evaluation
We repeatedly apply $B^\pi$ on the Function Approximation of $V:\mathcal{N}\rightarrow\mathbb{R}$. This operates on a Markov Reward Proces,s meaning we have no enumeration of states and no access to the transition probabilities.

We specify a sampling probability distribution of 'source states'. The sample pairs of (state $s'$, reward $r$) from each state. We can utilise these to estimate $E[r + \gamma\cdot V(s')]$ by averaging over the sampled pairs.  

### Finite-Horizon Approx DP
We can similarly generalize Backward Induction DP Algorithms. Each time steps' Value Function is a Funciton Approximation. Each time step will also have a seperate MRP/MDP representation that is responsible for sampling the next steps (state, reward) pair.
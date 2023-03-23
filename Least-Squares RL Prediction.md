#ReinforcementLearning 
The direct solution of the MRP Value Function using simple linear algebra operations is known as Least-Squares (abbreviated as LS) solution.

### Least-Squares [[Monte-Carlo]]
For the case of linear function approximation, the loss function for Batch MC Prediction with data $\left[\left(S_i, G_i\right) \mid 1 \leq i \leq n\right]$ is:
$$
\mathcal{L}(\boldsymbol{w})=\frac{1}{2 n} \cdot \sum_{i=1}^n\left(\sum_{j=1}^m \phi_j\left(S_i\right) \cdot w_j-G_i\right)^2=\frac{1}{2 n} \cdot \sum_{i=1}^n\left(\phi\left(S_i\right)^T \cdot \boldsymbol{w}-G_i\right)^2
$$
We set the gradient of this loss function to 0 , and solve for $\boldsymbol{w}^*$. This yields:
$$
\sum_{i=1}^n \boldsymbol{\phi}\left(S_i\right) \cdot\left(\boldsymbol{\phi}\left(S_i\right)^T \cdot \boldsymbol{w}^*-G_i\right)=0
$$
We can calculate the solution $\boldsymbol{w}^*$ as $\boldsymbol{A}^{-1} \cdot \boldsymbol{b}$, where the $m \times m$ Matrix $\boldsymbol{A}$ is accumulated at each data pair $\left(S_i, G_i\right)$ as:
$$
\boldsymbol{A} \leftarrow \boldsymbol{A}+\boldsymbol{\phi}\left(S_i\right) \cdot \boldsymbol{\phi}\left(S_i\right)^T \text { (i.e., outer-product of } \boldsymbol{\phi}\left(S_i\right) \text { with itself) }
$$
and the $m$-Vector $\boldsymbol{b}$ is accumulated at each data pair $\left(S_i, G_i\right)$ as:
$$
\boldsymbol{b} \leftarrow \boldsymbol{b}+\boldsymbol{\phi}\left(S_i\right) \cdot G_i
$$

The[[ Sherman-Morrison Formula]] incremental inverse for $\boldsymbol{A}$ is as follows:
$$
\left(\boldsymbol{A}+\boldsymbol{\phi}\left(S_i\right) \cdot \boldsymbol{\phi}\left(S_i\right)^T\right)^{-1}=\boldsymbol{A}^{-1}-\frac{\boldsymbol{A}^{-1} \cdot \boldsymbol{\phi}\left(S_i\right) \cdot \boldsymbol{\phi}\left(S_i\right)^T \cdot \boldsymbol{A}^{-1}}{1+\boldsymbol{\phi}\left(S_i\right)^T \cdot \boldsymbol{A}^{-1} \cdot \boldsymbol{\phi}\left(S_i\right)}
$$

### Least-Squares [[Temporal-Difference]]
For the case of linear function approximation, the loss function for Batch TD Prediction with data $\left[\left(S_i, R_i, S_i^{\prime}\right) \mid 1 \leq i \leq n\right]$ is:
$$
\mathcal{L}(\boldsymbol{w})=\frac{1}{2 n} \cdot \sum_{i=1}^n\left(\boldsymbol{\phi}\left(S_i\right)^T \cdot \boldsymbol{w}-\left(R_i+\gamma \cdot \phi\left(S_i^{\prime}\right)^T \cdot \boldsymbol{w}\right)\right)^2
$$
We set the semi-gradient of this loss function to 0 , and solve for $\boldsymbol{w}^*$. This yields:
$$
\sum_{i=1}^n \boldsymbol{\phi}\left(S_i\right) \cdot\left(\boldsymbol{\phi}\left(S_i\right)^T \cdot \boldsymbol{w}^*-\left(S_i+\gamma \cdot \boldsymbol{\phi}\left(S_i^{\prime}\right)^T \cdot \boldsymbol{w}^*\right)\right)=0
$$
We can calculate the solution $\boldsymbol{w}^*$ as $\boldsymbol{A}^{-1} \cdot \boldsymbol{b}$, where the $m \times m$ Matrix $\boldsymbol{A}$ is accumulated at each atomic experience $\left(S_i, R_i, S_i^{\prime}\right)$ as:
$$
\boldsymbol{A} \leftarrow \boldsymbol{A}+\boldsymbol{\phi}\left(S_i\right) \cdot\left(\boldsymbol{\phi}\left(S_i\right)-\gamma \cdot \boldsymbol{\phi}\left(S_i^{\prime}\right)\right)^T \text { (note the Outer-Product) }
$$
and the $m$-Vector $\boldsymbol{b}$ is accumulated at each atomic experience $\left(S_i, R_i, S_i^{\prime}\right)$ as:
$$
\boldsymbol{b} \leftarrow \boldsymbol{b}+\boldsymbol{\phi}\left(S_i\right) \cdot R_i
$$
With [[Sherman-Morrison Formula]] incremental inverse, we can reduce the computational complexity from $O\left(m^3\right)$ to $O\left(m^2\right)$, as follows:
$$
\left(\boldsymbol{A}+\boldsymbol{\phi}\left(S_i\right) \cdot\left(\boldsymbol{\phi}\left(S_i\right)-\gamma \cdot \boldsymbol{\phi}\left(S_i\right)\right)^T\right)^{-1}=\boldsymbol{A}^{-1}-\frac{\boldsymbol{A}^{-1} \cdot \boldsymbol{\phi}\left(S_i\right) \cdot\left(\boldsymbol{\phi}\left(S_i\right)-\gamma \cdot \boldsymbol{\phi}\left(S_i^{\prime}\right)\right)^T \cdot \boldsymbol{A}^{-1}}{1+\left(\boldsymbol{\phi}\left(S_i\right)-\gamma \cdot \boldsymbol{\phi}\left(S_i^{\prime}\right)\right)^T \cdot \boldsymbol{A}^{-1} \cdot \boldsymbol{\phi}\left(S_i\right)}
$$


### Least-Squares [[TD(Lambda) Prediction]]
For the case of linear function approximation, the loss function for Batch TD Prediction with data $\left[\left(S_i, R_i, S_i^{\prime}\right) \mid 1 \leq i \leq n\right]$ is:
$$
\mathcal{L}(\boldsymbol{w})=\frac{1}{2 n} \cdot \sum_{i=1}^n\left(\boldsymbol{\phi}\left(S_i\right)^T \cdot \boldsymbol{w}-\left(R_i+\gamma \cdot \phi\left(S_i^{\prime}\right)^T \cdot \boldsymbol{w}\right)\right)^2
$$
We set the semi-gradient of this loss function to 0 , and solve for $\boldsymbol{w}^*$. This yields:
$$
\sum_{i=1}^n \boldsymbol{\phi}\left(S_i\right) \cdot\left(\boldsymbol{\phi}\left(S_i\right)^T \cdot \boldsymbol{w}^*-\left(S_i+\gamma \cdot \boldsymbol{\phi}\left(S_i^{\prime}\right)^T \cdot \boldsymbol{w}^*\right)\right)=0
$$
We can calculate the solution $\boldsymbol{w}^*$ as $\boldsymbol{A}^{-1} \cdot \boldsymbol{b}$, where the $m \times m$ Matrix $\boldsymbol{A}$ is accumulated at each atomic experience $\left(S_i, R_i, S_i^{\prime}\right)$ as:
$$
\boldsymbol{A} \leftarrow \boldsymbol{A}+\boldsymbol{\phi}\left(S_i\right) \cdot\left(\boldsymbol{\phi}\left(S_i\right)-\gamma \cdot \boldsymbol{\phi}\left(S_i^{\prime}\right)\right)^T \text { (note the Outer-Product) }
$$
and the $m$-Vector $\boldsymbol{b}$ is accumulated at each atomic experience $\left(S_i, R_i, S_i^{\prime}\right)$ as:
$$
\boldsymbol{b} \leftarrow \boldsymbol{b}+\boldsymbol{\phi}\left(S_i\right) \cdot R_i
$$
With Sherman-Morrison incremental inverse, we can reduce the computational complexity from $O\left(m^3\right)$ to $O\left(m^2\right)$, as follows:
$$
\left(\boldsymbol{A}+\boldsymbol{\phi}\left(S_i\right) \cdot\left(\boldsymbol{\phi}\left(S_i\right)-\gamma \cdot \boldsymbol{\phi}\left(S_i\right)\right)^T\right)^{-1}=\boldsymbol{A}^{-1}-\frac{\boldsymbol{A}^{-1} \cdot \boldsymbol{\phi}\left(S_i\right) \cdot\left(\boldsymbol{\phi}\left(S_i\right)-\gamma \cdot \boldsymbol{\phi}\left(S_i^{\prime}\right)\right)^T \cdot \boldsymbol{A}^{-1}}{1+\left(\boldsymbol{\phi}\left(S_i\right)-\gamma \cdot \boldsymbol{\phi}\left(S_i^{\prime}\right)\right)^T \cdot \boldsymbol{A}^{-1} \cdot \boldsymbol{\phi}\left(S_i\right)}
$$
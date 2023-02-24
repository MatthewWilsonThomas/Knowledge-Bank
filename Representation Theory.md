#Mathematics 
#GroupTheory 
#Algebra 

A representation of a group $G$ is a group homomorphism $\rho: G \rightarrow \mathrm{GL}(V)$ where $\mathrm{GL}(V)$ is the group of automorphisms over a finite dimensional vector space $V$. The dimension $d_\rho$ of the representation $\rho$ is the dimension of $V$. A subspace $W \subseteq V$ is invariant iff $\forall g \in G, \rho(g)(W) \subseteq W$. If the only invariant subspaces are $\{0\}$ and $V$, we say that $\rho$ is irreducible. Two representations $\rho: G \rightarrow \operatorname{GL}\left(V_\rho\right)$ and $\tau: G \rightarrow \mathrm{GL}\left(V_\tau\right)$ of $G$ are equivalent or isomorphic iff there is an isomorphism $\psi: V_\rho \rightarrow V_\tau$ such that $\tau(g)=\psi \circ \rho(g) \circ \psi^{-1}$ for any $g \in G$. Given a representation $\rho$, we define the character $\chi_\rho$ by $\chi_\rho(g)=\operatorname{tr}(\rho(g))$
It can be shown that any finite group $G$ has only a finite number of irreducible pairwise non-isomorphic representations. More precisely, if we denote $\hat{G}$ a complete set of such representations and $V_\rho$ and $d_\rho$ the associated vector space and dimension (for any $\rho \in \hat{\mathrm{G}}$ ), we also know the followin inequality:
$$
\frac{1}{|G|} \sum_{\rho \in \hat{\mathrm{G}}} d_\rho \chi_\rho(g)=\delta_{g, 1}
$$
In particular for $g=1$, because $\chi_\rho(1)=\operatorname{tr}\left(I_{d_\rho}\right)=d_\rho$, we have:
$$
|G|=\sum_{\rho \in \hat{\mathrm{G}}} d_\rho{ }^2
$$
For each $\rho$, we can choose a basis of $V_\rho$ and then $\rho(g)$ is represented by a matrix of size $d_\rho$. Again, in view of the above formula, we can group all the coefficients $\left(\rho_{i j}(g)\right)_{1 \leq i, j \leq d_\rho, g \in G}$ in a square matrix of dimension $|G|$. To make this matrix unitary, we add the requirement that each $\rho(g)$ is unitary. We will see that it is always possible to choose the basis such that this requirement is satisfied. Once such a basis is chosen and when no confusion is possible, we will also denote $\rho(g)$ the matrix representation of $\rho(g)$ in this basis.


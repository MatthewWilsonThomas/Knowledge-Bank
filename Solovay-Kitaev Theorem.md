#QuantumComputing 

In quantum information and computation, the Solovay-Kitaev theorem says, roughly, that if a set of single-qubit quantum gates generates a dense subset of $SU(2)$, then that set can be used to approximate any desired quantum gate with a relatively short sequence of gates.

### Statement
Let $\mathcal{G}$ be a finite set of elements in $S U(2)$ containing its own inverses (so $g \in \mathcal{G}$ implies $g^{-1} \in \mathcal{G}$ ) and such that the group $\langle\mathcal{G}\rangle$ they generate is dense in $SU(2)$. Consider some $\varepsilon>0$. Then there is a constant $c$ such that for any $U \in SU(2)$, there is a sequence $S$ of gates from $\mathcal{G}$ of length $O\left(\log ^c(1 / \varepsilon)\right)$ such that $\|S-U\| \leq \varepsilon$. That is, $S$ approximates $U$ to operator norm error. ${ }^{[2]}$

### Proof
Suppose we have an approximation $U_{n-1} \in \mathrm{SU}(2)$ such that $\left\|U-U_{n-1}\right\| \leq \varepsilon_{n-1}$. Our goal is to find a sequence of gates approximating $U U_{n-1}^{-1}$ to $\varepsilon_n$ error, for $\varepsilon_n<\varepsilon_{n-1}$. By concatenating this sequence of gates with $U_{n-1}$, we get a sequence of gates $U_n$ such that $\left\|U-U_n\right\| \leq \varepsilon_n$
The key idea is that commutators of elements close to the identity can be approximated "better". Specifically, for $V, W \in \mathrm{SU}(2)$ satisfying $\|V-I\| \leq \delta_1$ and $\|W-I\| \leq \delta_1$ and approximations $\tilde{V}, \tilde{W} \in \mathrm{SU}(2)$ satisfying $\|V-\tilde{V}\| \leq \delta_2$ and $\|W-\tilde{W}\| \leq \delta_2$, then
$$
\left\|V W V^{-1} W^{-1}-\tilde{V} \tilde{W} \tilde{V}^{-1} \tilde{W}^{-1}\right\| \leq O\left(\delta_1 \delta_2\right)
$$
where the big $O$ notation hides higher-order terms. One can naively bound the above expression to be $O\left(\delta_2\right)$, but the group commutator structure creates substantial error cancellation.

We use this observation by rewriting the expression we wish to approximate as a group commutator $U U_{n-1}^{-1}=V_{n-1} W_{n-1} V_{n-1}^{-1} W_{n-1}^{-1}$. This can be done such that both $V_{n-1}$ and $W_{n-1}$ are close to the identity (since $\left\|U U_{n-1}^{-1}-I\right\| \leq \varepsilon_{n-1}$ ). So, if we recursively compute gate sequences approximating $V_{n-1}$ and $W_{n-1}$ to $\varepsilon_{n-1}$ error, we get a gate sequence approximating $U U_{n-1}^{-1}$ to the desired better precision $\varepsilon_n$ with $\varepsilon_n$. We can get a base case approximation with constant $\varepsilon_0$ by brute-force computation of all sufficiently long gate sequences.
#Mathematics 
#Algebra
#GroupTheory

Given a [[group]] $G$, a [[subgroup]] $H\leq G$, and a set $X$, we say a function $f:G\rightarrow X$ hides the subgroup $H$ if for all $g_1, g_2 \in G, f(g_1) = f(g_2)$ if and only if $g_1H = g_2H$. Equivalently, $f$ is constant on the [[coset]]s of $H$, while it is different between the different cosets of $H$. 

### Hiddern Subgroup 
Let $G$ be a group, $X$ a finite set, and $f: G \rightarrow X$ a function that hides a subgroup $H \leq G$. The function $f$ is given via an oracle, which uses $O(\log |G|+\log |X|)$ bits. Using information gained from evaluations of $f$ via its oracle, determine a generating set for $H$.

There is a efficient quantum algorithm for solving HSP over finite Abelian groups in time polynomial in $\log |G|$. Shor's algorithm applies a particular case of this quantum algorithm.

For arbitrary groups, it is known that the hidden subgroup problem is solvable using a polynomial number of evaluations of the oracle. However, the circuits that implement this may be exponential in $\log |G|$, making the algorithm overall not efficient; efficient algorithms must be polynomial in the number of oracle evaluations and running time. The existence of such an algorithm for arbitrary groups is open. Quantum polynomial time algorithms exist for certain subclasses of groups, such as semi-direct products of some Abelian groups.

To solve the problem for finite Abelian groups, the 'standard' approach to this problem involves: the creation of the quantum state $\frac{1}{\sqrt{|G|}} \sum_{x \in G}|x\rangle \otimes|f(x)\rangle$, a subsequent quantum Fourier transform to the left register, after which this register gets sampled. 
This approach has been shown to be insufficient for the hidden subgroup problem for the symmetric group. 
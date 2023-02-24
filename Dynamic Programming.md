#Algorithm 
#ReinforcementLearning
#Planning 

All the Dynamic Programming algorithms are build on the concept of Fixed-Points.

### Fixed-Points
The fixed-point of a function $f:\chi\rightarrow\chi$ (for some arbitrary domain $\chi$) is a value $x\in\chi$ s.t. $x = f(x)$.
Some algorithms have multiple fixed-points, some have none. The DP algorithms are based on functions with a unique fixed-point.

To be certain that we have a unique fixed-point we rely on the Banach Fixed-Point Theorem.

### Banach Fixed-Point Theorem
Let $\chi$ be a non-empty set equipped with a complete metric $d:\chi\times\chi\rightarrow\mathbb{R}$. Let $f:\chi\rightarrow\chi$ be s.t. there exists an $L\in[0, 1)$ s.t. $d(f(x_1), f(x_2))\leq L\cdot d(x_1, x_2)\quad\forall x_1, x_2\in \chi$. Then:
- There exists a unique fixed-point $x^*\in\chi$, i.e. $x^* = f(x^*)$.
- For any x0∈χ and sequence $[x_i|i=0,1,2,...]$ defined as $x_i+1=f(x_i)$ for all $i=0,1,2,...$:

$$

\lim_{i\rightarrow\infty} x_i = x^*

$$
So if $f(x)$ is a contraction we have a unique fixed-point.
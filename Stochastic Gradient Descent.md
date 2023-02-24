#Algorithm 
#GradientDescent
Stochastic Gradient Descent is a type of Gradient Descent which processes 1 training example per iteration. Hence, the parameters are updated after every iteration. Making it faster than gradient descent. If there are many training examples then this can have a very large overhead as you hvae to do many iterations. 

Algorithm:
![[Pasted image 20230209122933.png]]

This algorithm does not converge but will flucate around the global minimum. Thus to ensure convergence you should slowly alter the learning rate. 
#Algorithm 
#GradientDescent
This is a type of gradient descent which processes all the training examples for each iteration of gradient descent. But if the number of training examples is large, then batch gradient descent is computationally very expensive. Hence if the number of training examples is large, then batch gradient descent is not preferred. Instead, we prefer to use stochastic gradient descent or mini-batch gradient descent.

Algorithm: 
![[Pasted image 20230209123453.png]]

The convergence of Batch Descent is a straight line towards the minimum. If the cost function is convex then it converges to the global minimum. If it is not convex then it will converge to the local minimum which has no guarentee of being the global minimum. 
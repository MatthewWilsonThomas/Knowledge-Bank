#Algorithm 
#GradientDescent
This is a type of gradient descent which works faster than both batch gradient descent and stochastic gradient descent. Here _b_ examples where _b<m_ are processed per iteration. So even if the number of training examples is large, it is processed in batches of b training examples in one go. Thus, it works for larger training examples and that too with lesser number of iterations.

Algorithm:
![[Pasted image 20230209123756.png]]
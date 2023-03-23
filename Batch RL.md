#ReinforcementLearning 

Learning occurs in a granularly incremental manner, by updating the Value Function after each unit of experience. It doesn’t have to be this way—one can develop RL algorithms that take an entire batch of experiences (or in fact, all of the experiences that one could possibly get), and learn the Value Function directly for that entire batch of experiences. A key idea here is that if we know in advance what experiences data we have (or will have), and if we collect and organise all of that data, then we could directly (i.e., not incrementally) estimate the Value Function for that experiences data set. This approach to RL is known as Batch RL (versus the basic RL algorithms we covered in the previous chapters that can be termed as Incremental RL).


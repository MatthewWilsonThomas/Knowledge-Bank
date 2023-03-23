#ReinforcementLearning 

We consider the standard [[Q-Learning]] algorithm but adjust it so that the Q-Learning updates are sourced from an [[Experience Replay]] memory, rather than from a behaviour policy derived from the current Q-Value estimate. 

There were two key problems with [[Off-Policy Control]] TD methods with deep learning function approximation:
1. The sequences of states made available to deep learning through trace experiences are highly correlated, whereas deep learning algorithms are premised on data samples being independent.
2. The data distribution changes as the RL algorithm learns new behaviours, whereas deep learning algorithms are premised on a fixed underlying distribution (i.e., stationary).

Experience-Replay serves to smooth the training data distribution over many past behaviours, effectively resolving the correlation issue as well as the non-stationary issue. Hence, Experience-Replay is a powerful idea for Off-Policy TD Control.



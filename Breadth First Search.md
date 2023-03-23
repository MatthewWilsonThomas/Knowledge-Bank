#Algorithm 
#DiscreteMathematics 

The breadth-first search (BFS) algorithm is used to search a tree or graph data structure for a node that meets a set of criteria. It starts at the tree’s root or graph and searches/visits all nodes at the current depth level before moving on to the nodes at the next depth level. Breadth-first search can be used to solve many problems in graph theory.

The basic idea is to start with all nodes unvisited and an empty queue (nodes that will be visited in the queue order). Then we start at a given node, add all the adjacent nodes to the queue, marking them as visited as we go, then shift the current node to the queue(1) node, i.e. next node to be visited, adding all the adjacent nodes to the end of the queue. You can see all the nodes from the starting node will be visited before we move onto nodes from the first seen node. 

This can be extended to disconnected nodes by having a check at the end to ensure all the nodes have been visited, if they have not been we can randomly initialise the BFS at a new node, repeating until all graph segments have been discovered and visited. 

### Pseudocode algorithm
```
Breadth_First_Search( Graph, X )
Here, Graph is the graph that we already have and X is the source node

Let Q be the queue 
Q.enqueue( X ) // Inserting source node X into the queue  
Mark X node as visited.

While ( Q is not empty )  
Y = Q.dequeue( ) // Removing the front node from the queue

Process all the neighbors of Y, For all the neighbors Z of Y  
If Z is not visited, Q. enqueue( Z ) // Stores Z in Q  
Mark Z as visited
```

### Implementation
```python
# Python3 Program to print BFS traversal
# from a given source vertex. BFS(int s)
# traverses vertices reachable from s.
from collections import defaultdict
 
# This class represents a directed graph
# using adjacency list representation
 
 
class Graph:
 
    # Constructor
    def __init__(self):
 
        # default dictionary to store graph
        self.graph = defaultdict(list)
 
    # function to add an edge to graph
    def addEdge(self, u, v):
        self.graph[u].append(v)
 
    # Function to print a BFS of graph
    def BFS(self, s):
 
        # Mark all the vertices as not visited
        visited = [False] * (max(self.graph) + 1)
 
        # Create a queue for BFS
        queue = []
 
        # Mark the source node as
        # visited and enqueue it
        queue.append(s)
        visited[s] = True
 
        while queue:
 
            # Dequeue a vertex from
            # queue and print it
            s = queue.pop(0)
            print(s, end=" ")
 
            # Get all adjacent vertices of the
            # dequeued vertex s. If a adjacent
            # has not been visited, then mark it
            # visited and enqueue it
            for i in self.graph[s]:
                if visited[i] == False:
                    queue.append(i)
                    visited[i] = True

# Create a graph given in
# the above diagram
g = Graph()
g.addEdge(0, 1)
g.addEdge(0, 2)
g.addEdge(1, 2)
g.addEdge(2, 0)
g.addEdge(2, 3)
g.addEdge(3, 3)
 
print("Following is Breadth First Traversal"
      " (starting from vertex 2)")
g.BFS(2)
 
# This code is contributed by Neelam Yadav
```



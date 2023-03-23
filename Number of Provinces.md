#Problem 
[[Depth First Search]]

There are `n` cities. Some of them are connected, while some are not. If city `a` is connected directly with city `b`, and city `b` is connected directly with city `c`, then city `a` is connected indirectly with city `c`.

A **province** is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the `ith` city and the `jth` city are directly connected, and `isConnected[i][j] = 0` otherwise.

Return _the total number of **provinces**_.

```python
import numpy as np

class Solution:
    def findCircleNum(self, isConnected: List[List[int]]) -> int:
        number_provinces: int = 0
        visited: List[bool] = [False]*len(isConnected)

        neighbors = lambda x, loc: [ind for ind, val in enumerate(x) if val == 1 and ind != loc]

        to_visit = lambda x: [ind for ind, val in enumerate(x) if val == False]

        def dfs(visited, v):
            visited[v] = True

            # Recur for all the vertices
            # adjacent to this vertex
            for neighbour in neighbors(isConnected[v], v):
                if visited[neighbour] is False:
                    dfs(visited, neighbour)

        while len(to_visit(visited)) > 0:
            not_seen = to_visit(visited)
            number_provinces += 1
            dfs(visited, not_seen[0])

        return number_provinces
```
#Problem 
[[Depth First Search]]

On a 2D plane, we place `n` stones at some integer coordinate points. Each coordinate point may have at most one stone.

A stone can be removed if it shares either **the same row or the same column** as another stone that has not been removed.

Given an array `stones` of length `n` where `stones[i] = [xi, yi]` represents the location of the `ith` stone, return _the largest possible number of stones that can be removed_.

```python
class Solution:
    def removeStones(self, stones: List[List[int]]) -> int:

        
        graphX: Dict[List] = defaultdict(list)
        graphY: Dict[List] = defaultdict(list)

        for x,y in stones:
            graphX[x].append(y)
            graphY[y].append(x)

        def dfs(xo,yo):
            nonlocal visited
            if (xo,yo) not in visited:
                visited.add((xo,yo))
                for neiY in graphX[xo]:
                    dfs(xo,neiY)
                for neiX in graphY[yo]:
                    dfs(neiX,yo)
        
        connectedComponent: int = 0
        visited: set = set()

		# i.e. you only ever need to leave the root of a DFS tree in the grid. You can remmove all other nodes. 
        for x,y in stones:
            if (x,y) not in visited:
                dfs(x,y)
                connectedComponent += 1
        
        return len(stones)-connectedComponent
        ```
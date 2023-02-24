#Problem
[[Depth First Search]]

```python
from typing import *

class Solution:
    def findBall(self, grid: List[List[int]]) -> List[int]:
        ROWS, COLS = len(grid), len(grid[0])
        pos = [c for c in range(COLS)]
        
        for row in range(ROWS):
            for col in range(COLS):
                if pos[col] >= 0: # when can move down
                    if grid[row][pos[col]] == 1: # if can go right e.g. \
                        if pos[col] + 1 < COLS and grid[row][pos[col] + 1] == 1: # \\ and right is the same -> move right
                            pos[col] += 1
                        else:
                            pos[col] = -1 # \/ or \| blocked
                    elif grid[row][pos[col]] == -1: # if can go left e.g. /
                        if pos[col] > 0 and grid[row][pos[col] - 1] == -1: # // and left is the same -> move left
                            pos[col] -= 1
                        else:
                            pos[col] = -1
            
        return pos
```
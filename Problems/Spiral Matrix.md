#Problem
#Simulation

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:

        width = len(matrix[0])
        height = len(matrix)

        loc = [0, 0]
        direction = [0, 1]

        path = []

        while len(path) < width * height:
            path.append(matrix[loc[0]][loc[1]])
            matrix[loc[0]][loc[1]] = 120

            # Next step
            n_loc = [i + j for i, j in zip(loc, direction)]
            if (0 <= n_loc[0] < height) and (0 <= n_loc[1] < width) and (matrix[n_loc[0]][n_loc[1]] != 120):
                loc = n_loc
            else:
                # Change direction then update
                direction[0], direction[1] = direction[1], -direction[0]
                n_loc = [i + j for i, j in zip(loc, direction)]
                loc = n_loc

        return path
```
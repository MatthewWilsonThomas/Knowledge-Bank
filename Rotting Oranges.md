#Problem 
[[Breadth First Search]]

You are given an `m x n` `grid` where each cell can have one of three values:

-   `0` representing an empty cell,
-   `1` representing a fresh orange, or
-   `2` representing a rotten orange.

Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange becomes rotten.

Return _the minimum number of minutes that must elapse until no cell has a fresh orange_. If _this is impossible, return_ `-1`.

```python
class Solution:
    def bfs(self, grid: List[List[int]],
            queue: List[Tuple[int, int]],
            number_steps: int,
            number_oranges: int,
            number_rotten: int) -> int:
        elems_in_queue: int = len(queue)

        # No further adjacent oranges to be found and the number of rotten oranges is less than the number of oranges means all the oranges cannot be turned rotten, i.e. -1
        if queue == [] and number_rotten != number_oranges:
            return -1

        number_steps += 1        

        # For all previously found oranges, turn them rotten and find any connected oranges
        for _ in range(elems_in_queue):
            current = queue.pop(0)
            i = current[0]
            j = current[1]

            if grid[i][j] != 2:
                grid[i][j] = 2
                number_rotten += 1

            # Append connected oranges to the initial queue
            if i + 1 < len(grid) and grid[i+1][j] == 1:  # Move down
                queue.append(tuple([i+1, j]))
            
            if i - 1 >= 0 and grid[i-1][j] == 1:             # Move up
                queue.append(tuple([i-1, j]))

            if j + 1 < len(grid[0]) and grid[i][j+1] == 1:   # Move right
                queue.append(tuple([i, j+1]))

            if j - 1 >= 0 and grid[i][j-1] == 1:             # Move left
                queue.append(tuple([i, j-1]))

        if number_rotten == number_oranges:
            return number_steps
        else:
            return self.bfs(grid, queue, number_steps, number_oranges, number_rotten)

    def orangesRotting(self, grid: List[List[int]]) -> int:
        queue: List[Tuple[int, int]] = []
        number_oranges: int = 0
        number_rotten: int = 0
        number_steps: int = 0


        for i, row in enumerate(grid):
            for j, elem in enumerate(row):
                if elem != 0:
                    number_oranges += 1

                if elem == 2:
                    number_rotten += 1
                     # Append connected oranges to the initial queue
                    if i + 1 < len(grid) and grid[i+1][j] == 1:
                            queue.append(tuple([i+1, j]))
                    
                    if i - 1 >= 0 and grid[i-1][j] == 1:
                        queue.append(tuple([i-1, j]))

                    if j + 1 < len(grid[0]) and grid[i][j+1] == 1:
                        queue.append(tuple([i, j+1]))

                    if j - 1 >= 0 and grid[i][j-1] == 1:
                        queue.append(tuple([i, j-1]))
        if number_rotten == number_oranges:
            return number_steps

        print(queue)

        return self.bfs(grid, queue, number_steps, number_oranges, number_rotten)
```
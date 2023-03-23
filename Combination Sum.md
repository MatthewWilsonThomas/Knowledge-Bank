#Problem 
[[Depth First Search]]

Given an array of **distinct** integers `candidates` and a target integer `target`, return _a list of all **unique combinations** of_ `candidates` _where the chosen numbers sum to_ `target`_._ You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the 

frequency

 of at least one of the chosen numbers is different.

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        ans = []
        n = len(candidates)
        def dfs(cur, cur_sum, idx):                       # try out each possible cases
            if cur_sum > target: 
                return                   # this is the case, cur_sum will never equal to target
            if cur_sum == target: 
                ans.append(cur)
                return # if equal, add to `ans`
            for i in range(idx, n): 
                dfs(cur + [candidates[i]], cur_sum + candidates[i], i) # DFS

        dfs([], 0, 0)
        return ans     
```
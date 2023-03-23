#Problem 
[[Depth First Search]]

Given an array `nums` of distinct integers, return _all the possible permutations_. You can return the answer in **any order**.

```python
class Solution:
    def dfs(self, nums, path, res):
        if not nums:
            res.append(path)
            return # backtracking
        for i in range(len(nums)):
            self.dfs(nums[:i]+nums[i+1:], path+[nums[i]], res)

    def permute(self, nums: List[int]) -> List[List[int]]: 
        res = []
        self.dfs(nums, [], res)
        return res
```
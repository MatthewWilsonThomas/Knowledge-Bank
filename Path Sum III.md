#Problem 
[[Depth First Search]]

Given the `root` of a binary tree and an integer `targetSum`, return _the number of paths where the sum of the values along the path equals_ `targetSum`.

The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:

    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> int:
        count = 0
        if not root:
            return count
        q = deque([(root, [root.val])])
        while q:
            length = len(q)
            for i in range(length):
                node, path_till_node = q.popleft()
                # Search for target sum in current path
                Sum = 0
                for i in reversed(path_till_node):
                    Sum += i
                    if Sum == targetSum:
                        count += 1
                # append the queue with child nodes and list of values till them
                if node.left:
                    q.append((node.left, path_till_node + [node.left.val]))
                if node.right:
                    q.append((node.right, path_till_node + [node.right.val])) 
        return count
```
Use of deque to speed up BFS was necessary to avoid time out errors.
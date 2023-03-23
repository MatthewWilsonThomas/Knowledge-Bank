#Problem
#Stack

Given a string `s` which represents an expression, _evaluate this expression and return its value_. 

The integer division should truncate toward zero.

You may assume that the given expression is always valid. All intermediate results will be in the range of `[-231, 231 - 1]`.

```python
import numpy as np

class Solution:
    def calculate(self, s: str) -> int:

        stack, curr, op = [], 0, '+'
        for c in s + '+':
            if c == ' ':
                continue
            elif c.isdigit():
                curr = (curr * 10) + int(c)
            else:
                if op == '-':
                    stack.append(-curr)
                elif op == '+':
                    stack.append(curr)
                elif op == '/':
                    stack.append(int(stack.pop() / curr))
                elif op == '*':
                    stack.append(int(stack.pop()) * curr)
                curr, op = 0, c
        return np.sum(stack)
```
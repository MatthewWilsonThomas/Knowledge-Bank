#Problem 

Given two non-negative integers `num1` and `num2` represented as strings, return the product of `num1` and `num2`, also represented as a string.

```python
class Solution:
    def multiply(self, num1: str, num2: str) -> str:

		convert_to_num = lambda x: np.sum([int(bit)*(10**(len(x)-loc-1)) for loc, bit in enumerate(x)])

        int1: int = convert_to_num(num1)
        int2: int = convert_to_num(num2)

        return str(int1 * int2)```
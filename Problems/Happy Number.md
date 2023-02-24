#Problem
#Hashing

```python
def sumSquareDigits(n):
    sumsquare = 0
    while(n):
        sumsquare += (n % 10) * (n % 10)
        n = int(n / 10)
    return sumsquare

class Solution:
    def isHappy(self, n: int) -> bool:
        
        seen = set()
        seen.add(n)

        while(True):
            n = sumSquareDigits(n)

            if n == 1:
                return True
            if n in seen:
                return False
            
            seen.add(n)
```
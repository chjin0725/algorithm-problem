
# 풀이
```python3
class Solution:
    def subtractProductAndSum(self, n: int) -> int:
        p = 1
        s = 0
        while n != 0:
            digit = n%10
            n = n//10
            p *= digit
            s += digit
        
        return p - s
```

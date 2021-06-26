
# 풀이
- xor을 이용하면 간단하게 풀린다.
```python3
class Solution:
    def hammingDistance(self, x: int, y: int) -> int:
        ans = 0
        temp = x^y
        for _ in range(32):
            ans += 1&temp
            temp >>= 1
        
        return ans
```

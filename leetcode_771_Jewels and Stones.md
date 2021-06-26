
# 풀이
- set을 쓰면 된다.
```python3
class Solution:
    def numJewelsInStones(self, J: str, S: str) -> int:
        jewel = set()
        for j in J:
            jewel.add(j)
            
        ans = 0
        for s in S:
            if s in jewel:
                ans += 1
        
        return ans
```

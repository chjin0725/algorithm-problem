
# 풀이
- 이진 탐색으로 풀 수 있다.
```python3
class Solution:
    def isPerfectSquare(self, num: int) -> bool:
        if num == 1:
            return True
        if num == 2 or num == 3:
            return False
        
        lo = 1
        hi = num//2
        
        while lo <= hi:
            mid = (lo + hi)//2
            square = mid**2
            if square == num:
                return True
            elif square < num:
                lo = mid + 1
            else:
                hi = mid - 1
        
        return False
```

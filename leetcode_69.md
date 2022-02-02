- 이진탐색 문제
```python3
class Solution:
    def mySqrt(self, x: int) -> int:
        if x < 2:
            return x
        
        lo = 1
        hi = x//2
        while lo <= hi:
            mid = (lo + hi)//2
            
            if mid**2 > x:
                hi = mid-1
            elif mid**2 < x:
                lo = mid+1
            else:
                return mid
        
        return hi
```

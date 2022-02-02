- 이진탐색 문제
```python3
# The isBadVersion API is already defined for you.
# def isBadVersion(version: int) -> bool:

class Solution:
    def firstBadVersion(self, n: int) -> int:
        lo = 1
        hi = n
        
        while lo < hi:
            mid = (lo+hi)//2
            
            if isBadVersion(mid) == False: ## 이 때만 lo가 증가하기 때문에 lo는 False이거나 첫번째 True이다
                lo = mid + 1                # 즉, 1 ~ lo까지는 전부 False이거나 1~lo-1까지는 전부 False이다
                                            # 그래서 return은 lo를 하는 것임.
            elif isBadVersion(mid) == True:
                hi = mid
        
        return lo
```

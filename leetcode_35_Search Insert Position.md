
# 풀이
- 그냥 bisect 구현하는 문제임.
```python3
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        lo = 0
        hi = len(nums)
        
        while lo < hi:
            mid = (lo + hi)//2
            if nums[mid] < target:
                lo = mid + 1
            else:
                hi = mid
            
        return lo
```

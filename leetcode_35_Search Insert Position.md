# 문제
![leetcode_35](https://user-images.githubusercontent.com/51700219/77845279-9981e680-71e8-11ea-8f24-59c54d8c1d4c.png)
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

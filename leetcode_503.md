```python
class Solution:
    def nextGreaterElements(self, nums: List[int]) -> List[int]:
        if not nums:
            return nums
        
        res = [0] * len(nums)
        
        max_index = 0
        for i in range(1, len(nums)):
            if nums[max_index] < nums[i]:
                max_index = i
        
        s = [max_index]
        cur_index = max_index
        for _ in range(len(nums)):
            while s and nums[s[-1]] <= nums[cur_index]:
                s.pop()
            
            if s:
                res[cur_index] = nums[s[-1]]
            else:
                res[cur_index] = -1
            
            s.append(cur_index)
            cur_index = (cur_index + len(nums) - 1)%len(nums)
            
        return res
```

  - 스택을 쓰는 문제.

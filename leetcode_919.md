- dp문제인데 꽤 어렵다.
- circular의 의미를 생각해봐야 한다. 즉, 배열안에서 maximum sum subarray를 찾는 것 뿐만 아니라 prefix + suffix가 최대가 되는 경우도 고려해야 한다.
- prefix + suffix가 최대가 되는 경우는 배열의 전체 합 - minimum sum subarray 이다.
- 또한 edge case도 고려해줘야 한다. 모든 수가 음수인 배열의 경우.

```python3
class Solution:
    def maxSubarraySumCircular(self, nums: List[int]) -> int:
        cur_middle = nums[0]
        middle_sum = nums[0]
        for i in range(1, len(nums)):
            if cur_middle < 0:
                cur_middle = nums[i]
            else:
                cur_middle += nums[i]
                
            middle_sum = max(middle_sum, cur_middle)
        
        cur_min = nums[0]
        min_sum = nums[0]
        for i in range(1, len(nums)):
            if cur_min < 0:
                cur_min += nums[i] 
            else:
                cur_min = nums[i]
                
            min_sum = min(min_sum, cur_min)
        
        return max(middle_sum, sum(nums) - min_sum) if middle_sum > 0 else middle_sum
```

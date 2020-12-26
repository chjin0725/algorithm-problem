```python
class Solution:
    def waysToMakeFair(self, nums: List[int]) -> int:
        l = [0,0]
        r = [0,0]
        
        for i in range(len(nums)-1,0,-1):
            if i%2 == 0:
                r[0] += nums[i]
            else:
                r[1] += nums[i]
                
        ans = 0
        
        if (l[0] + r[0]) == (l[1] + r[1]):
            ans += 1
            
        for i in range(1, len(nums)):
            if i%2 == 0:
                l[0] += nums[i-1]
                r[0] -= nums[i]
                
                if (l[0] + r[0]) == (l[1] + r[1]):
                    ans += 1
            else:
                l[1] += nums[i-1]
                r[1] -= nums[i]
                
                if (l[0] + r[0]) == (l[1] + r[1]):
                    ans += 1
           
        return ans

```

```python
class Solution:
    def shipWithinDays(self, weights: List[int], D: int) -> int:
        size_nums = math.ceil(len(weights)/D)
        max_sum = 0
        for i in range(size_nums):
            max_sum += weights[i]
        for i in range(size_nums, len(weights) - size_nums + 1):
            temp = max_sum - weights[i - size_nums] + weights[i]
            max_sum = max(max_sum, temp)
        
        lo = 1
        hi = max_sum
        
        def check(capacity):
            cur_cap = 0
            cur_day = 1
            
            for w in weights:
                if capacity < w:
                    return False
                elif cur_cap + w <= capacity:
                    cur_cap += w
                else:
                    cur_cap = w
                    cur_day += 1
                    
                    if cur_day > D:
                        return False
            return True
        
        while lo <= hi:
            mid = (lo + hi)//2
            
            if check(mid):
                hi = mid - 1
            else:
                lo = mid + 1
                
        return lo
```

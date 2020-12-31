```python
class Solution:
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        output = []
        
        def dfs(num, sum_so_far, nums_so_far):
            nums_so_far.append(num)
            sum_so_far += num
            if len(nums_so_far) > k or num >= 10 or sum_so_far > n:
                return
            
            if len(nums_so_far) == k :
                if sum_so_far == n:
                    output.append(nums_so_far)
                    return
                else:
                    return
                
                
                
            
            for i in range(num+1 , 10):
                dfs(i, sum_so_far, nums_so_far[:])
                
        for j in range(1,10):
            dfs(j, 0, [])
        
        return output
```

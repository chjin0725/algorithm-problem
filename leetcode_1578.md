```python
class Solution:
    def minCost(self, s: str, cost: List[int]) -> int:
        
        i = 0
        ans = 0
        
        def search_cost(i):
            sum_cost = cost[i]
            max_cost = cost[i]
            
            while i < len(s)-1 and s[i] == s[i+1]:
                i += 1
                sum_cost += cost[i]
                max_cost = max(max_cost, cost[i])
            
            return i, sum_cost - max_cost
        
        while i < len(s)-1:
            if s[i] == s[i+1]:
                i, temp= search_cost(i)
                ans += temp
            else:
                i += 1
                
        
        return ans
```

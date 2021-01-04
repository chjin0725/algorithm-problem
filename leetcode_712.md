```python
class Solution:
    def minimumDeleteSum(self, s1: str, s2: str) -> int:
        dp = [0]*(len(s1)+1)
        for i in range(1, len(dp)):
            dp[i] = dp[i-1] + ord(s1[i-1])
            
        pre_dp = dp[:]    
        for j in range(len(s2)):
            dp[0] = pre_dp[0] + ord(s2[j])
            for i in range(len(s1)):
                if s1[i] == s2[j]:
                    dp[i+1] = pre_dp[i]
                else:
                    dp[i+1] = min(dp[i] + ord(s1[i]), dp[i+1] + ord(s2[j]))
            pre_dp = dp[:]    
        return dp[-1] if dp else 0
```

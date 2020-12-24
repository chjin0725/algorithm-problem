```python
class Solution:
    def numSplits(self, s: str) -> int:
        num_char_r = dict()
        for c in s:
            if c in num_char_r:
                num_char_r[c] += 1
            else:
                num_char_r[c] = 1
                
        ans = 0
        num_char_l = set()
        for i in range(len(s)-1):
            num_char_l.add(s[i])
            
            num_char_r[s[i]] -= 1
            
            if num_char_r[s[i]] == 0:
                del num_char_r[s[i]]
            
            if len(num_char_l) == len(num_char_r):
                ans += 1
            
        return ans
```

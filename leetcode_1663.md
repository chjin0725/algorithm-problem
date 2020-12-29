```python
class Solution:
    def getSmallestString(self, n: int, k: int) -> str:
        s = 'abcdefghijklmnopqrstuvwxyz'
        chr_index = {i : s[i] for i in range(len(s))}
        
        ans = ['a' for _ in range(n)]
        str_value = n
        
        i = n-1
        
        while True:
            if k - str_value > 0:
                index = (k - str_value) if (k - str_value) < 25 else 25
                ans[i] = chr_index[index]
                str_value += index
                
                i -= 1
            else:
                return ''.join(ans)
```

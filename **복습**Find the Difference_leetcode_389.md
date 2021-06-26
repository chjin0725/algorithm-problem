
# 풀이
- A ^ B ^ A = A ^ A ^ B = B 를 이용
```python3
class Solution:
    def findTheDifference(self, s: str, t: str) -> str:
        ch_num = 0
        for c in t+s:
            ch_num ^= ord(c)
        
        
        return chr(ch_num)
```

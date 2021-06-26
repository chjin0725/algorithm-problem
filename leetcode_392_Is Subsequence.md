

# 풀이
- 너무 쉬워서 설명은 생략하겠다.
```python3
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        length_s = len(s)
        length_t = len(t)
        if length_s == 0:
            return True
        if length_t == 0:
            if length_s == 0:
                return True
            else:
                return False
        i = 0
        for c in t:
            if s[i] == c:
                i += 1
                if i == length_s:
                    return True
        return False
        
```

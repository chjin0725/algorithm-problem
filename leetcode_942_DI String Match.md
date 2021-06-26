

# 풀이
- D이면 가장 작은것을 넣고 I이면 가장 큰 것을 넣는다.
```python3
class Solution:
    def diStringMatch(self, S: str) -> List[int]:
        n = len(S)
        l = 0
        h = n
        ans = [0]*(n+1)
        for i in range(n-1, -1, -1):
            if S[i] == 'I':
                ans[i+1] = h
                h -= 1
            else:
                ans[i+1] = l
                l += 1
        ans[0] = l
        
        return ans
```

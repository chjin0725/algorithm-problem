- count dp 문제이다
- count dp에서는 max, min같은 함수는 쓰이지 않는다.

```python3
class Solution:
    def numDecodings(self, s: str) -> int:
        numbers = set()
        for n in range(1,27):
            numbers.add(str(n))
            
        two_back = int(s[0] in numbers)
        
        if len(s) == 1:
            return two_back
        
        one_back = two_back*(s[1] in numbers) + (s[:2] in numbers)
        
        for i in range(2, len(s)):
            cur = two_back*(s[i-1:i+1] in numbers) + one_back*(s[i] in numbers)
            two_back = one_back
            one_back = cur
        
        return one_back
```

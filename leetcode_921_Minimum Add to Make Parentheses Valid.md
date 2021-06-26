

# 풀이
- 스택으로 푸는 문제
- 지겹게 본 유형
```python3
class Solution:
    def minAddToMakeValid(self, S: str) -> int:
        s = []
        ans = 0
        for c in S:
            if c == '(':
                s.append(c)
            else:
                if s:
                    s.pop()
                else:
                    ans += 1
        
        return ans + len(s)
```
# 다른 풀이
- 괄호 유형이 소괄호 하나이기 때문에 굳이 스택을 쓸 필요 없다.( 사실 소괄호 말고 다른거 있어도 스택안쓰고 할 수 있음)
```python3
class Solution:
    def minAddToMakeValid(self, S: str) -> int:
        num_left = 0
        ans = 0
        for c in S:
            if c == '(':
                num_left += 1
            else:
                if num_left:
                    num_left -= 1
                else:
                    ans += 1
        
        return ans + num_left
```

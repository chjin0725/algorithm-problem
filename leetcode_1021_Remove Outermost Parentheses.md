
# 풀이
- 괄호문제를 좀 변형한 문제. 어렵진 않음.
```python3
    def removeOuterParentheses(self, S: str) -> str:
        if S == '':
            return ''
        s = 0
        temp = []
        start = 0
        for i in range(len(S)):
            if S[i] == '(':
                s+=1
            else:
                s-=1
                if not s:
                    temp.append(S[start+1:i])
                    start = i+1        
        return ''.join(temp)  
```

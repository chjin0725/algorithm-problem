
# 풀이
- 괄호문제랑 비슷하다. 스택을 써주면 된다
- ``#``이 나올때마다 스택에서 pop한다.
```python3
class Solution:
    def backspaceCompare(self, S: str, T: str) -> bool:
        s1 = []
        s2 = []
        for c in S:
            if c != '#':
                s1.append(c)
            elif s1:
                s1.pop()
        for c in T:
            if c != '#':
                s2.append(c)
            elif s2:
                s2.pop()        
                
        return s1==s2
```

# 다른 풀이
- 문자열을 뒤에서부터 본다.
- 뒤에서 부터 보는것 까지는 알았는데 어떻게 비교할지가 생각이 안났다. 너무 졸림.
- 졸리니까 머리가 잘 안돌아간다. 역시 공부는 낮에 해야돼.
- 뒤에서 부터 보는 방식을 생각하면 조금 복잡하지만 각 경우들을 따지면 풀수는 있다.
```python3
class Solution:
    def backspaceCompare(self, S: str, T: str) -> bool:
        len_s = len(S)
        len_t = len(T)
        p1 = len_s - 1
        p2 = len_t - 1
        back_s = 0
        back_t = 0
        while True:
            while p1 >= 0 and (back_s or S[p1] == '#'):
                back_s += 1 if S[p1] == '#' else -1
                p1 -= 1
            while p2 >= 0 and (back_t or T[p2] == '#'):
                back_t += 1 if T[p2] == '#' else -1
                p2 -= 1
                
            if p1 < 0 or p2 < 0:
                return p1==p2==-1
            elif S[p1] == T[p2]:
                p1 -= 1
                p2 -= 1
            else:
                return False
                
```

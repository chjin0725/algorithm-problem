# 문제

# 풀이
- 어렵지 않은 문제
- 다만 코드를 좀 깔끔하게 짜보려고 노력해봤다.
```python3
class Solution:
    def stringShift(self, s: str, shift: List[List[int]]) -> str:
        n = len(s)
        move = 0
        for e in shift:
            move += -(-1)**e[0]*e[1]    
        move %= n
        return s[n-move:] + s[:n-move]
```
- move로 한쪽방향으로 움직여야 하는 횟수를 계산한다.
- ``move += -(-1)**e[0]*e[1]``와 같이 함으로써 e[0]가 0이면 e[1]을 빼주고 e[0]가 양수이면 e[1]을 더해주도록 한다. if문을 안써서 깔끔해 보인다. 
- move가 음수여도 ``move %= n`` 을 해도 된다. 왼쪽으로 2칸 움직이는 것은 오른쪽으로 n-2칸 움직이는 거랑 같기 때문.
- 만일 move가 -2라면 ``move %= n``이후에는 n-2가 될 것이다.

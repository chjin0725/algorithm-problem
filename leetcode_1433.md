```python
from collections import Counter
class Solution:
    def checkIfCanBreak(self, s1: str, s2: str) -> bool:
        s1 = Counter(s1)
        s2 = Counter(s2)
        
        check = set()
        diff = 0
        for c in 'abcdefghijklmnopqrstuvwxyz':
            diff += s1[c] - s2[c]
            
            if diff:
                check.add(diff > 0)
        
        
        return len(check) < 2
```

 - 정렬하지 않고 풀 수 있다.
 - 심지어 one pass로 풀 수 있다.
 - a 부터 z까지 개수의 차이를 계산했을 때, 한 문자열이 다른 문자열을 break 가능하다면 개수의 차이는 계속 0이상 혹은 계속 0이하로 유지되야 한다.
 - 그러므로 check의 크기가 2가 되면 중간에 개수의 차이가 뒤집어 졌다는 것이므로 False가 된다.

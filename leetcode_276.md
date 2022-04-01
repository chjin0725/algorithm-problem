- counting dp 문제이다.
- 같은색이 연속으로 3번 발생하면 안된다. 
- 그렇다면 가능한 경우를 생각해보면 현재 울타리의 색깔이 이전과 다른 경우, 이전과 같지만 이전전과는 다른경우가 가능하다.
- 이걸 점화식으로 생각해보면 답을 얻을 수 있다.


```python3
class Solution:
    def numWays(self, n: int, k: int) -> int:
        if n == 1:
            return k
        
        pre = k
        pre_pre = 1
        
        for _ in range(n-2):
            cur = pre*(k-1) + pre_pre*(k-1)
            pre_pre = pre
            pre = cur
        
        return pre*k
```

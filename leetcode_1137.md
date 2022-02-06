- 피보나치 수열문제
- dp문제이다
- 이전3개의 값만 유지하면 되기 때문에 배열을 쓸 필요는 없음

```python3
class Solution:
    def tribonacci(self, n: int) -> int:
        if n == 0:
            return 0
        if n <= 2:
            return 1
        
        cur = 1
        p = 1
        pp = 0
        
        for _ in range(3,n+1):
            temp = cur + p + pp
            pp = p
            p = cur
            cur = temp
        
        return cur
```

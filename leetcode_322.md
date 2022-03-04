- dp 문제이다. 최소값을 찾는 문제이고 subproblem들의 solution이 다음 ploblem의 solution을 구하는데 이용되는 구조이다(optimal substructure).
- 일단 state variable은 coin과 amount이다.
- coin의 index i와 어떤 amount값 x가 주어졌을 때 dp[i][x]는 0~i 까지의 coin과 x가 input으로 주어졌을 때의 solution이다.
- 이를 이용하여 recurrence relation을 생각해보면 dp[i][x] = min(dp[i][x] , dp[i-1][x-i] + 1) 이다. 즉, 현재 코인 i에 대해서 이전 코인까지의 solution들 중에 amount가 x-i일 때의 solution에서
현재 코인 i를 하나 사용한 것과 비교해보는 것이다.
- 여기서 dp배열값을 계산할 때 i-1번째 행만 사용되므로 dp배열은 그냥 1차배열로 구현해도 된다.

```python3
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [float('inf')]*(amount + 1)
        dp[0] = 0
        
        for coin in coins:
            for i in range(coin, amount+1):
                dp[i] = min(dp[i], dp[i-coin] + 1)
        
        return dp[-1] if dp[-1] != float('inf') else -1
```

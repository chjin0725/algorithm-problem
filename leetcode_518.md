- count dp문제이다.
- dp에서는 3가지만 기억하면 된다. state variable, recurrence relation, base case.
- state variable은 input으로 정해진다. input이 배열이면 그 인덱스가 state variable이 되고 input이 상수 k이면 0~k 혹은 1~k가 state variable이 된다.
- recurrence relation을 구할 때는 "dp[i][j] = input이 i,j까지만 주어졌을때의 solution"임을 기억하면 된다.

```python3
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = [[0 for _ in range(amount+1)] for _ in range(len(coins)+1)]
        
        for i in range(len(dp)):
            dp[i][0] = 1
        
        for i in range(1, len(dp)):
            coin = coins[i-1]
            for j in range(1, len(dp[0])):
                if j - coin >= 0:
                    dp[i][j] = dp[i-1][j] + dp[i][j-coin]
                else:
                    dp[i][j] = dp[i-1][j]
        
        return dp[-1][-1]
```

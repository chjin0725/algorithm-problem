- dp문제.
- dp[i]는 i번쨰 계단까지 오는데 필요한 cost의 최소값이다.
- i까지의 최소비용를 알기 위해서는 i-1까지의 최소비용과 i-2까지의 최소비용을 알아야 한다. 이게 dp문제에서 나타나는 구조임.
- 굳이 dp배열을 만들 필요는 없고 i-1과 i-2만 알고 잇으면 되므로 변수 2개만 가지고 있으면 된다.

```python3
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        pre = cost[1]
        pre_pre = cost[0]
        
        for i in range(2, len(cost)):
            temp = min(pre+cost[i], pre_pre+cost[i])
            pre_pre = pre
            pre = temp
        
        return min(pre, pre_pre)
```

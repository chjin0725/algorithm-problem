
# 풀이
- 처음에는 그리디인지 dp인지 헷갈렸는데 몇가지 테스트 케이스를 생각해보니 그리디로는 안풀린다.
- dp이다. 
```python3
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        if len(cost) == 2:
            return min(cost[0], cost[1])
        dp = [0]*len(cost)
        dp[0] = cost[0]
        dp[1] = cost[1]
        
        for i in range(2,len(cost)):
            dp[i] = cost[i] + min(dp[i-1], dp[i-2])
        
        return min(dp[-2], dp[-1])
```
- 이렇게 풀 경우 메모리 사용량이 높게 나온다.
# 다른 풀이
- dp라는 배열을 만들 필요 없이 cost자체를 쓰면 된다(in place algorithm)
```python3
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        if len(cost) == 2:
            return min(cost[0], cost[1])
        
        
        for i in range(2,len(cost)):
            cost[i] = cost[i] + min(cost[i-1], cost[i-2])
        
        return min(cost[-2], cost[-1])
```
- in palce algorithm은 메모리 사용량을 줄일 수 있지만 input자체를 변경하게 되는 단점이 있다.


# 풀이
- dp 같으면서 greedy인 문제이다.
- greedy하게 풀면 된다.
- prices[i]의 가격이 prices[i-1]의 가격 보다 작으면 이전에 산 것을 prices[i-1]에 팔고 prices[i]를 구매한다.
```python3
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if not prices:
            return 0
        ans = 0
        num_stock = len(prices)
        
        buy = pre = prices[0]
        for i in range(1, num_stock):
            if prices[i] < pre:
                ans += (pre - buy)
                buy = prices[i]
            pre = prices[i]
        ans += prices[-1] - buy     
        
        return ans
```
- ``ans += prices[-1] - buy`` 이부분은 [1,2,3,4,5] 같이 가격이 계속 증가하는 경우를 위해서 한다.
# 다른 풀이
- 알고보니 같은날에 주식을 팔고 사는게 가능한 거였다.
- 그런거라면 그냥 구매한 주식보다 가격이 더 높은 주식이 나오는 순간 팔고 바로 사는식으로 해도 됨
```python3
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        ans = 0
        num_stock = len(prices)

        for i in range(1, num_stock):
            if prices[i] > prices[i-1]:
                ans += (prices[i] - prices[i-1])
                
        return ans
```

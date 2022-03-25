- 188번 문제에서 조금만 바뀐 문제이다.
- 코드도 조금만 바꾸면 된다.
- 일단 거래는 무한번 가능하므로 최대 거래량은 prices배열의 길이에 의해 결정된다. 다만 sell하고 나서는 한번 쉬어주어야 하는 부분을 고려해 줘야 한다.
- 즉 최대 거래량 k는 (len(prices)+1)//3 이다.
- 또한 sell하고 한번 쉬어줘야 하기 때문에 cur[j]를 계산할 때 pre[j-2]번째 값을 이용해야 한다.

```python3
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        pre = [0]*(len(prices)+2)
        i = 2
        ans = float('-inf')
        k = (len(prices) +1)//3
        
        for _ in range(k):
            
            # buy
            cur = [float('-inf')]*(len(prices)+2)
            for j in range(i, len(prices)+2):
                cur[j] = max(pre[j-2] - prices[j-2], cur[j-1])
            i += 1
            pre = cur
            
            # sell
            cur = [float('-inf')]*(len(prices)+2)
            for j in range(i,len(prices)+2):
                cur[j] = max(pre[j-1] + prices[j-2], cur[j-1])
            i += 2
            pre = cur
            
            ans = max(ans, pre[-1])
            
        return max(0, ans)
```

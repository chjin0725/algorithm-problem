- dp문제. hard문제이고 꽤 오래된 문제이다.
- 정수k와 prices배열이 주어진다. 그러므로 k와 prices에 대해서 for문을 도는 식으로 풀릴 수 있을 것이다.
- 일단 최대 k번 거래가 가능하다고 하였고 거래라는 것은 한번의 구매와 한번의 판매로 이루어진다.
- 좀 더 쉽게 생각하기 위해 k를 다시 정의하자. k를 구매회수와 판매회수라고 생각하자. 즉 입력으로 k가 2로 주어졌다면 구매와 판매를 두번씩 하므로 다시 정의한 k는 4가 될것이다.
- k가 홀수일 때는 구매를 하고 k가 짝수일때는 판매를 한다.
- 즉, dp[k][i]는 i번째 까지 봤을 때 k-1번째 까지 구매(혹은 판매)를 하고 k번째에서 판매(혹은 구매)를 할 때 이윤의 최대값으로 정의할 수 있다.
- 그러면 k는 홀수일 때 dp[k][i] = max(dp[k-1][i-1] - prices[i], dp[k][i-1]) 이다. k는 짝수면 dp[k][i] = max(dp[k-1][i-1] + prices[i], dp[k][i-1])이다.
- 다만 k x len(prices) 사이즈의 dp행렬을 만들 필요는 없다. 그냥 이전 행만 있으면 되기 때문.

```python3
class Solution:
    def maxProfit(self, k: int, prices: List[int]) -> int:
        pre = [0]*(len(prices)+1)
        i = 1
        ans = float('-inf')
        
        for _ in range(k):
            
            # buy
            cur = [float('-inf')]*(len(prices)+1)
            for j in range(i, len(prices)+1):
                cur[j] = max(pre[j-1] - prices[j-1], cur[j-1])
            i += 1
            pre = cur
            
            # sell
            cur = [float('-inf')]*(len(prices)+1)
            for j in range(i,len(prices)+1):
                cur[j] = max(pre[j-1] + prices[j-1], cur[j-1])
            i += 1
            pre = cur
            
            ans = max(ans, pre[-1])
            
        return max(0, ans)
```

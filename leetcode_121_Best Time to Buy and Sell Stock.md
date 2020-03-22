# 문제
![leetcode_121](https://user-images.githubusercontent.com/51700219/77223311-bee67300-6b9e-11ea-9375-ae82ad04d73e.png)
# 풀이
- 처음에는 dp인 느낌이 들었다.
- i번째에서 solution을 가지고 있을 때 i+1번째에서는 어떻게 solution을 구할 수 있을까를 생각해 보았다.
- i+1번째 원소에서 0~i번째 원소들을 다 빼보고 그 중에 최솟값을 i번째 solution과 비교해 보면 될 것이다.
- 그러나 이건 n^2의 방법이다. 거의 부르트포스 이다.
- 생각해보니 0~i번째 원소들을 전부 다 빼볼 필요 없이 이중에서 최솟값하고만 뺴보면 된다.
- 알고보니 greedy였다.
```python3
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if not prices: ## empty list
            return 0
        
        buy = prices[0]
        ans = 0
        
        for i in range(1, len(prices)):
            if buy > prices[i]:
                buy = prices[i]
            ans = max(ans, prices[i] - buy)
        
        return ans
            
```

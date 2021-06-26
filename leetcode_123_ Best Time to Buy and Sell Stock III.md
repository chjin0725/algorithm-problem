
# 풀이
- 121번 문제는 최대 거래수가 1번이었는데 이건 최대 거래수가 2번이다.
- 처음에는 0 <= i <= length(prices)-1인 i에 대해서 0~i까지를 첫번쨰 거래, i+1 ~(length -1)까지를 두번째 거래로 나눈 다음에 최대 거래수가 1번 일때의
알고리즘을 각각의 첫번째, 두번째 거래에 적용하는 것을 생각했다.
- 이건 n^2의 시간이 걸린다.
- discuss의 제목만 봤는데 n의 시간을 가지는 알고리즘도 있다. 그래서 어떻게 n의 시간으로 풀 수 있을지 생각해 보았다.
- 0~i까지는 i가 커질때마다 그때그때의 새로운 maximum profit(이걸 솔루션 이라 하자)을 o(1)의 시간으로 구할 수 있다. 그냥 최대 거래수가 한번인 알고리즘을 적용하면 된다.
- 그러나 i~length-1까지의 부분은 i가 커질때 마다 o(1)의 시간으로 구할수가 없다. 매번 최대거래수가 한번인 알고리즘을 새로 적용해야 한다.
- i~length-1까지의 부분이 문제인데 이 부분을 어떻게 해야 시간을 줄일 수 있을까?
- 생각하다보니  i~length-1까지의 부분은 거꾸로 보는 방법이 생각났다. 즉, 솔루션을 구할때 i부터 보는게 아니라 length-1부터 보는 것이다. 여기서 뒤에서
보는 것이므로 i는 감소한다.
- 즉  length-1만을 봤을때의 솔루션을 구하고 그 다음으로  length-2~length-1까지의 부분, 그다음은 length-3~length-1 부분을 보는 것이다. 다만 여기서는
판매할 주식의 최대값을 갱신해야 한다.
- 이런식으로 i~length-1부분의 솔루션은 미리 계산해서 리스트에 저장해둔다.
```python3
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        length = len(prices)
        
        if length == 0 or length == 1:
            return 0
        
        sell = prices[-1]
        
        right_max = [0]*(length+1)

        
        for i in range(length-1, -1, -1):
            if sell < prices[i]:
                sell = prices[i]
            right_max[i] = max(right_max[i+1], sell - prices[i])
        
        ans = right_max[0]
        left_max = 0
        buy = prices[0]
        for i in range(length):
            if buy > prices[i]:
                buy = prices[i]
            left_max = max(left_max, prices[i] - buy)
            ans = max(ans, left_max + right_max[i+1])
            
        return ans
```

- interview cake를 공부할 때 어려운 문제는 조건을 오나하하여 먼저 풀어보고 이를 확장시키라는 조언이 있었다.
- 즉 어려운 문제는 조건이 까다롭기 떄문에 어려운 것인데 이 조건을 완화한 버전으로 풀어보라는 것.
- 이 문제를 풀기전에 121번 문제에서 최대 거래수가 1번인 경우를 먼저 풀었었다.
- 그 때문에 이 문제를 풀 때 해결책을 생각하기가 쉬웠던 것 같다. 실제 알고리즘도 121번 문제를 응용한 수준이다.
- 어려운 문제는 조건을 완화해서 풀어보는 것을 꼭 기억하자.
- 처음으로 리트코드 하드문제를 거의 내 힘으로 풀었다.

- dp문제이다. dp문제를 풀 때는 state variable, recurrence relation과 dp함수의 리턴값, base case를 차례로 찾아야 한다.
- 먼저 해당 문제에서 각 state를 정의하기 위해서는 multiplier의 index와 leftmost(혹은 rightmost)를 몇번 선택했는지 알아야하므로 총 2개의 state variable이 필요하다.
- 즉 dp배열은 2차원 배열이다.
- 다음으로 recurrence relation과 dp배열의 리턴값을 정의해야 한다.
- 만일 dp[i][left]를 "i번쨰 multiplier와 left개의 leftmost 숫자를 택했을 때 얻을 수 있는 최대 score라 하면?
- recurrence relation이 정의되지 않는다. 즉 do[i][left]와 그 이전 값들을 아는 것으로는 dp[i+1][left], dp[i+1][left+1]을 알 수 없다.
- 이럴 경우 relation을 잘못 정의한 것이다. 이 문제에서는 recurrence relation이 반대로 되어야 한다.
- 즉, dp[i+1][left]와 dp[i+1][left+1]을 알아야 dp[i][left]를 알 수 있다. 이런걸 알려면 recurrence relation이 제대로 정의될 떄 까지 dp[i][left]의 정의를 바꿔가면서 생각해볼 수 밖에 없는 듯.

```python3
class Solution:
    def maximumScore(self, nums: List[int], multipliers: List[int]) -> int:
        m, n = len(multipliers), len(nums)
        dp = [[0]*(m+1) for _ in range(m+1)]
        
        for i in range(m-1, -1, -1):
            for left in range(i, -1, -1):
                right = n-1 - (i-left)
                multi = multipliers[i]
                
                dp[i][left] = max(multi*nums[left] + dp[i+1][left+1], multi*nums[right] + dp[i+1][left])
                
        return dp[0][0]
```

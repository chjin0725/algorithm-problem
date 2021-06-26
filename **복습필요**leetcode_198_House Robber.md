
# 풀이
- dp문제이다. i-1번째 솔루션을 알 고 있을때 i번째 솔루션을 어떻게 구할지를 여러 케이스를 손으로 풀어가며 생각해본다. 이게 핵심!!!
- 인접한 집은 털 수 없으므로 i번째 솔루션을 구할때는 i-1번째와 i-2번째 두 개를 참고해야 한다.
```python3
class Solution:
    def rob(self, nums: List[int]) -> int:
        
        n = len(nums)
        if n == 0:
            return 0
        if n == 1:
            return nums[0]
        dp = [0]*n
        dp[0] = nums[0]
        dp[1] = max(nums[1], nums[0])
        
        for i in range(2,n):
            dp[i] = max(dp[i-1], dp[i-2] + nums[i])
            
        return dp[-1]
```
- dp 배열을 안쓰고 변수 2개를 쓰면 공간복잡도를 상수로 둘 수 있다.
```python3
class Solution:
    def rob(self, nums: List[int]) -> int:
        
        n = len(nums)
        if n == 0:
            return 0
        if n == 1:
            return nums[0]
        dp = [0]*n
        pre_pre = nums[0]
        pre = max(nums[1], nums[0])
        
        for i in range(2,n):
            temp = max(pre, pre_pre + nums[i])
            pre_pre = pre
            pre = temp
            
        return pre
```

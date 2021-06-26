
# 풀이
- 왼쪽에서 오른쪽으로 숫자를 더하면서 볼 때 최소값을 구하면 된다.
- 즉 prefix sum의 최소값을 구하고 그것의 절대값 +1 을 한다.
- 단 모든 숫자가 0이상일 경우도 다룰 수 있게 해야 함.
```python3
class Solution:
    def minStartValue(self, nums: List[int]) -> int:
        temp = 0
        ans = 1
        for n in nums:
            temp += n
            if temp < 0:
                ans = max(ans, abs(temp) + 1)
        
        return ans
```

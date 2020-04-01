# 문제
![leetcode_1365](https://user-images.githubusercontent.com/51700219/78163020-b20d2d80-7482-11ea-90ef-8a199b5f6c95.png)
# 풀이
- 가장 먼저 떠오른 방법은 정렬이다. 정렬로 하면 간단히 풀 수 있다. 그래서 정답률이 높은 듯.
- 근데 정렬은 너무 간단하고 o(n)으로 풀 수 없을까 생각해 보았다. o(n)으로는 쉽지 않다.
- 떠오른 방법은 일단 nums의 숫자들의 빈도수를 세어주는 것이다.
```python3
class Solution:
    def smallerNumbersThanCurrent(self, nums: List[int]) -> List[int]:
        ans = [0]*len(nums)
        
        
        number_count = [0]*101
        dp = [0]*101
        for num in nums:
            number_count[num] += 1
        
        print(number_count)
        dp[0] = number_count[0]
        for i in range(1,len(dp)):
            dp[i] = dp[i-1] + number_count[i] 
        
        print(dp)
        for i in range(len(ans)):
            ans[i] = dp[nums[i]] - number_count[nums[i]]
        
        return ans
```
- number_count 는 nums에 나오는 숫자들의 빈도수를 계산한다.
- number_count를 가지고 dp는 누적개수를 구한다. dp[i]는 i이하인 것의 개수이다.(i "미만"이 아님)
- nums에 나오는 숫자의 범위가 0~100으로 제한되어 있기 때문에 가능한 방법이다.

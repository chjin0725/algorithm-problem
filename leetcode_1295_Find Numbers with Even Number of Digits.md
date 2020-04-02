# 문제
![leetcode_1295](https://user-images.githubusercontent.com/51700219/78253680-ba6f7200-752f-11ea-90cb-3fafdd43db98.png)

# 풀이
```python3
class Solution:
    def findNumbers(self, nums: List[int]) -> int:
        ans = 0
        for num in nums:
            num_digit = 0
            while num != 0:
                num //= 10
                num_digit += 1
            if num_digit%2 == 0:
                ans += 1
        return ans
```
- log10(n)에서 소수점 자리를 제거해도 n의 자리수를 구할 수 있다.

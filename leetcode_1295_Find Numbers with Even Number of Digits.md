

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
- log10(n)을  n의 자리수를 구할 수 있다.

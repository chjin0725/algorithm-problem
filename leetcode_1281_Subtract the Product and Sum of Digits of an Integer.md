# 문제
![leetcode_1281](https://user-images.githubusercontent.com/51700219/78254470-edfecc00-7530-11ea-9685-0758af97cb7d.png)
# 풀이
```python3
class Solution:
    def subtractProductAndSum(self, n: int) -> int:
        p = 1
        s = 0
        while n != 0:
            digit = n%10
            n = n//10
            p *= digit
            s += digit
        
        return p - s
```

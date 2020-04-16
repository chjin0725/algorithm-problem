# 문제
![leetcode_461](https://user-images.githubusercontent.com/51700219/79445322-7001f100-8017-11ea-9752-b32e1bcfc041.png)
# 풀이
- xor을 이용하면 간단하게 풀린다.
```python3
class Solution:
    def hammingDistance(self, x: int, y: int) -> int:
        ans = 0
        temp = x^y
        for _ in range(32):
            ans += 1&temp
            temp >>= 1
        
        return ans
```

# 문제
![leetcode_389](https://user-images.githubusercontent.com/51700219/81493679-677e9c80-92dd-11ea-821e-b5150f3e6938.png)
# 풀이
- A ^ B ^ A = A ^ A ^ B = B 를 이용
```python3
class Solution:
    def findTheDifference(self, s: str, t: str) -> str:
        ch_num = 0
        for c in t+s:
            ch_num ^= ord(c)
        
        
        return chr(ch_num)
```

# 문제
![leetcode_1304](https://user-images.githubusercontent.com/51700219/79143011-68fc9800-7df7-11ea-8cb9-ee74e671d83c.png)
# 풀이
```python3
class Solution:
    def sumZero(self, n: int) -> List[int]:
        ans = []
        if n%2 == 0:
            for i in range(1,int(n/2)+1):
                ans.append(i)
                ans.append(-i)
        else:
            for i in range(1,n//2+1):
                ans.append(i)
                ans.append(-i)
            ans.append(0)
        return ans
```

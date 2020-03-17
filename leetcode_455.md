# 문제
![leetcode_455](https://user-images.githubusercontent.com/51700219/76846734-50df3a80-6884-11ea-98de-1578b2106232.png)
# 풀이
- 읽자마자 그리디 문제인게 느껴지는 문제임.
- 뭔가 s가 가장큰 쿠키를 g가장 큰 아이에게 할당하면 될거 같음
- 만약 그렇게 할때 s가 가장큰 쿠키가 g가 가장큰 아이의 g보다 작다면? 을 생각하는데 핵심
- 그럴 경우 다음으로 가장큰 g에게 할당해야 할 것이다.
- 즉, s(j) >= g(i)를 만족하는 가장큰 g(i)에게 s(j)를 할당 한다.
```python3
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        g.sort()
        s.sort()
        num_kids = len(g)
        ans = 0
        
        for i in range(num_kids):
            if s:
                if s[-1] >= g[num_kids-1-i]:
                    ans += 1
                    s.pop()
            else:
                break
                
        return ans
```

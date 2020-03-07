# 문제
![leetcode1221](https://user-images.githubusercontent.com/51700219/76138794-c5002e00-608d-11ea-9783-2037dc4a85b2.png)
  - constraints
    - 1 <= s.length <= 1000
    - s[i] = 'L' or 'R'
    

# 풀이
<pre>
<code>
class Solution:
    def balancedStringSplit(self, s: str) -> int:
        num_R = 0
        num_L = 0
        ans = 0
        
        for c in s:
          if c == 'R':
            num_R += 1
            
          else:
            num_L += 1
            
          if num_R == num_L:
            ans += 1
            num_L = 0
            num_R = 0
            
        return ans
</pre>
</code>

## 다른 풀이
<pre>
<code>
class Solution:
    def balancedStringSplit(self, s: str) -> int:
        cnt = ans = 0
        for c in s:
            cnt += 1 if c =='L' else -1
            
            if cnt == 0:
                ans += 1
        
        return ans
</pre>
</code>

- 변수를 cnt하나만으로 계산해주고 있음.
- 이게 더 세련되보인다. 기억해두자.

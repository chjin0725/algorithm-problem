
# 풀이
- 0 이 나온 횟수와 1 이 나온 횟수를 세어주면서 계산한다.
- 현재 숫자와 이전숫자가 같을때랑 다를때로 나눠서 처리해준다.
```python3
class Solution:
    def countBinarySubstrings(self, s: str) -> int:
        count = {'0' : 0, '1' : 0}
        ans = 0
        count[s[0]] += 1
        for i in range(1, len(s)):
            temp = self.reverse_num(s[i])
            if s[i] == s[i-1]:
                count[s[i]] += 1
                if count[temp] > 0:
                    count[temp] -= 1
                    ans += 1
            else:
                if count[temp] > 0:
                    count[temp] -= 1
                    ans += 1
                    count[s[i]] = 1
        return ans
        
                    
            
    def reverse_num(self, c):
        if c == '0':
            return '1'
        else:
            return '0'
```

# 훨씬 쉽고 설명도 편한 풀이
- ``001100011'' 의 경우를 예로 설명하면 문자열을 순회하면서 연속되는 같은숫자의 개수를 세어준다
- 위의 예의 경우 [2,2,3,2] 이다.
- [2,2,3,2]를 순회하면서 현재값과 다음값 중 더 작은값을 ans에 더한다.
- 멋진 풀이인 듯.
```python3
class Solution:
    def countBinarySubstrings(self, s: str) -> int:
        num_consecutive = []
        count = 1
        for i in range(1,len(s)):
            if s[i] == s[i-1]:
                count += 1
            else:
                num_consecutive.append(count)
                count = 1
        num_consecutive.append(count)
        
        if len(num_consecutive) == 1:
            return 0
        else:
            ans = 0
            for i in range(len(num_consecutive)-1):
                ans += min(num_consecutive[i], num_consecutive[i+1])
            return ans
```

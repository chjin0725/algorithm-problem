- dp 문제이다.
- 다른 dp 문제들과는 다르게 최대 혹은 최소를 구하는 유형이 아니다. dp중에서는 보기 드문 유형이다.
- 다만 다른 dp문제에서 처럼 input에 대해서 iteration을 도는 것은 동일하다.
- 그리고 최대, 최소에 대한 언급은 없지만 그냥 보면 뭔가 dp같은 느낌이 든다. 왜냐하면 optimal substructure가 느껴지기 때문이다. 주어진 문자열에서 현재 index까지의 substring이 주어진 word로 구성가능한지
보려면 이전 index들 까지의 substring들이 주어진 word로 구성가능한지 봐야 하기 때문이다.

```python3
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        dp = [0]*len(s)
        
        for i in range(len(s)):
            for word in wordDict:
                if word[-1] == s[i] and (i - len(word)) >= -1 and s[i-len(word)+1 : i+1] == word and \
                ((i - len(word)) == -1 or dp[i - len(word)] == 1):
                    dp[i] = 1
                    break
        
        return dp[-1]
```

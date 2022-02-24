- 문제 링크 : https://leetcode.com/problems/longest-common-subsequence/
- state variable은 2개이다. 각 text에 대한 index 하나씩 총 2개.
- dp[i][j]는 text1은 i까지, text2는 j까지 봤을 때의 Longest Common Subsequence이다.
- dp[i][j] = max(dp[i-1][j], dp[i][j-1], dp[i-1][j-1] + int(text1[i] == text2[j])) 이다.
- dp[i-1][j-1]은 i-1과 j-1 까지 봤을 때의 Longest Common Subsequence이고 여기서 text1[i]와 text2[j]가 같으면 +1을 해준다.
- 다만 text[i] != text[j]라면 dp[i-1][j] 혹은 dp[i][j-1]과 같게 된다. 어차피 text1의 i번째 문자와 text2의 j번째 문자는 서로 다르기 때문에 Longest Common Subsequence는 바뀌지 않기 때문이다.
- 여기서 공간복잡도를 좀 더 최적화 하면 결국에는 dp행렬에서는 2개의 행만 필요하게 되므로 그냥 배열 2개만 가지고 구현해 줄 수 있다.

```python3
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        row = [0] * len(text2)
        row[0] = int(text1[0] == text2[0])
        
        for i in range(1, len(text2)):
            row[i] = max(row[i-1], int(text1[0] == text2[i]))
            
        for i in range(1, len(text1)):
            temp_row = [0] * len(text2)
            temp_row[0] = max(row[0], int(text1[i] == text2[0]))
            
            for j in range(1, len(text2)):
                temp_row[j] = max(temp_row[j-1], row[j], row[j-1] + int(text1[i] == text2[j]))
            
            row = temp_row
        
        return row[-1]
```



# 풀이
- dp문제이다.
- 아래그림 참고
- ![leetcode_1314_figure](https://user-images.githubusercontent.com/51700219/78421741-ece6af80-7694-11ea-9d31-dd15c986f8bc.png)
```python3
class Solution:
    def matrixBlockSum(self, mat: List[List[int]], K: int) -> List[List[int]]:
        m,n = len(mat),len(mat[0])
        dp = [[0]*n for _ in range(m)]
        
        dp[0][0] = mat[0][0]
        for r in range(1,m):
            dp[r][0] = dp[r-1][0] + mat[r][0]
        for c in range(1, n):
            sumc = 0
            for r in range(m):
                sumc += mat[r][c]
                dp[r][c] = sumc + dp[r][c-1]
                
        for r in range(m):
            for c in range(n):
                r_plus = min(r+K, m-1)
                c_plus = min(c+K, n-1)
                left = 0 if (c-K-1)<0 else dp[r_plus][c-K-1]
                up = 0 if (r-K-1)<0 else dp[r-K-1][c_plus]
                leftUp = 0 if (r-K-1)<0 or (c-K-1)<0 else dp[r-K-1][c-K-1]
                
                mat[r][c] = dp[r_plus][c_plus] - left - up + leftUp
        
        return mat
```
- dp[r][c] 는 0,0 부터 r,c까지 가로세로 길이가 r,c인 사각형에 속하는 원소의 합이다.
- dp자체는 문제의 답을 가지고 있지 않다. 다만 dp를 이용해서 문제의 답을 푼다.
- 시간복잡도, mn

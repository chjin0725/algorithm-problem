- 크게 어렵진 않은 dp문제이다.
- matrix[i][j]의 값이 1일 때 이를 포함하는 가장 큰 square의 한변의 길이는 matrix[i-1][j], matrix[i][j-1], matrix[i-1][j-1] 각각을 포함하는 가장 큰 square의 한변의 길이의 최소값 +1 이다.
- 예를 들어  matrix[i-1][j]를 포함하는 가장 큰 square의 한변의 길이가 3이라면 이는  matrix[i-1][j]기준으로 3의 길이만큼 떨어진 거리까지 주변 원소들의 값이 1임을 알려주는 것이기 때문이다.

```python3
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        m = len(matrix)
        n = len(matrix[0])
        
        ans = 0
        for r in range(m):
            if matrix[r][0] == '1':
                ans = 1
        
        for c in range(1, n):
            if matrix[0][c] == '1':
                ans = 1
        
        for r in range(1, m):
            for c in range(1, n):
                if matrix[r][c] == '1':
                    matrix[r][c] = str(min(int(matrix[r-1][c]), int(matrix[r][c-1]), int(matrix[r-1][c-1])) + 1)
                    ans = max(ans, int(matrix[r][c]))
        
        return ans**2
```

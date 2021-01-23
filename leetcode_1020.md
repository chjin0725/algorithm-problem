```python
class Solution:
    def numEnclaves(self, A: List[List[int]]) -> int:
        m = len(A)
        n = len(A[0])
        
        def dfs(r,c):
            
            if A[r][c] == 1:
                A[r][c] = 0
                for r2, c2 in [(r-1, c), (r+1, c), (r, c-1), (r, c+1)]:
                    if 0<=r2<m and 0<=c2<n:
                        dfs(r2,c2)
        
        for j in range(n):
            dfs(0,j)
            dfs(m-1,j)
        
        for i in range(1, m-1):
            dfs(i,0)
            dfs(i, n-1)
        
        return sum(list(map(sum,A)))
```

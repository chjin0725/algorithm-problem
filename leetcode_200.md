- 그냥 간단한 bfs, dfs 문제이다.

```python3
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        m = len(grid)
        n = len(grid[0])
        
        ans = 0
        for r in range(m):
            for c in range(n):
                if grid[r][c] == '1':
                    self.dfs(r,c,grid,m,n)
                    ans += 1
        return ans
    
    def dfs(self, r_s, c_s, grid, m, n):
        s = [(r_s, c_s)]
        
        while s:
            r,c = s.pop()
            grid[r][c] = '0'
            
            for r2,c2 in [(r-1,c), (r+1,c), (r,c-1), (r,c+1)]:
                if 0 <= r2 < m and 0 <= c2 < n and grid[r2][c2] == '1':
                    s.append((r2,c2))
```

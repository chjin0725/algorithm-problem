```python
class Solution:
    def findCircleNum(self, isConnected: List[List[int]]) -> int:
        visited = set()
        
        
        n = len(isConnected)
        
        ans = 0
        
        def dfs( i):
            s = [i]
            while s:
                cur = s.pop()
                visited.add(cur)
                
                for neighbor in range(n):
                    if cur != neighbor and neighbor not in visited and isConnected[cur][neighbor] == 1:
                        s.append(neighbor)
                
        for i in range(n):
            if i in visited:
                pass
            else:
                dfs(i)
                ans += 1
        
        return ans
```

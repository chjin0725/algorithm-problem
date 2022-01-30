- dfs 또는 union-find로 풀 수 있다.

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

```python3
class Solution:
    def findCircleNum(self, isConnected: List[List[int]]) -> int:
        root = [i for i in range(len(isConnected))]
        rank = [1 for _ in range(len(isConnected))]
        
        for r in range(len(isConnected)):
            for c in range(r, len(isConnected)):
                if isConnected[r][c] == 1:
                    self.union(root, rank, r, c)
        
        subsets = set()
        for i in range(len(isConnected)):
            subsets.add(self.find(root, i))
        
        return len(subsets)
        
    def find(self, root, x):
        if root[x] == x:
            return x
        root[x] = self.find(root, root[x])
        
        return root[x]
    
    def union(self, root, rank, x, y):
        root_x = self.find(root, x)
        root_y = self.find(root, y)
        
        if root_x != root_y:
            if rank[root_x] > rank[root_y]:
                root[root_y] = root_x
            elif rank[root_x] < rank[root_y]:
                root[root_x] = root_y
            else:
                root[root_y] = root_x
                rank[root_x] += 1
```

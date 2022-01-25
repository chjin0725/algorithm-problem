- source 노드에서 destination 노드로 가는 경로가 있는지 확인하는 문제.
- dfs 혹은 bfs를 쓰면 간단히 풀린다.

```python3
from collections import defaultdict
class Solution:
    def validPath(self, n: int, edges: List[List[int]], source: int, destination: int) -> bool:
        adj = defaultdict(list)
        for v1, v2 in edges:
            adj[v1].append(v2)
            adj[v2].append(v1)
        
        s = [source]
        visit = set()
        while s:
            cur = s.pop()
            visit.add(cur)

            if cur == destination:
                return True

            for neigh in adj[cur]:
                if neigh not in visit:
                    s.append(neigh)
                    visit.add(neigh)

        return False
```

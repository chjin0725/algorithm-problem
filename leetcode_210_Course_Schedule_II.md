 - directed graph에서 cycle이 있는지 알아내는 문제이다.
 - topological sort를 사용하면 쉽게 풀 수 있다.
 - 혹은 dfs를 쓴다면 아직 call stack에 있는 노드를 또 방문할 경우 cycle이 있다고 할 수 있는 점을 이용하여 풀 수도 있다.

```python3
from collections import deque, defaultdict
class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        indegree = [0]*numCourses
        out = defaultdict(list)
        q = deque()
        
        
        for v1, v2 in prerequisites:
            out[v2].append(v1)
            indegree[v1] += 1
        
        for v in range(numCourses):
            if indegree[v] == 0:
                q.append(v)
        
        ans = []
        cnt = 0
        while q:
            cur = q.popleft()
            ans.append(cur)
            
            for v in out[cur]:
                indegree[v] -= 1
                if indegree[v] == 0:
                    q.append(v)
            cnt += 1
            
        if cnt != numCourses:
            return []
        else:
            return ans
```

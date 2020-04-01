# 문제
![leetcode_994](https://user-images.githubusercontent.com/51700219/77844793-6178a480-71e4-11ea-8351-ee389bafb5e8.png)

# 풀이
- bfs를 이용하면 된다.
- 다만 어떻게 시간을 기록할 지에 대해서 생각이 잘 안났다.
- 매번 새로운 오렌지를 방문할 때마다 그 오렌지의 좌표뿐만 아니라 그 오렌지가 썩게된 시간도 같이 큐에 넣어주면 된다.
```python3
from collections import deque
class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        visited = set()
        q = deque()
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == 2:
                    q.appendleft((i,j,0)) # third element is the time orange rottend
        t = 0
        while q:
            i,j,t = q.popleft()
            if i-1>=0 and grid[i-1][j] == 1:
                grid[i-1][j] = 2
                q.append((i-1,j,t+1))
            if i+1 <= (len(grid)-1) and grid[i+1][j] == 1:
                grid[i+1][j] = 2
                q.append((i+1,j,t+1))
            if j-1>=0 and grid[i][j-1] == 1:
                grid[i][j-1] = 2
                q.append((i,j-1,t+1))
            if j+1 <= (len(grid[0])-1) and grid[i][j+1] == 1:
                grid[i][j+1] = 2
                q.append((i,j+1,t+1))
        
        for i in range(len(grid)):
            if 1 in grid[i]:
                return -1
        
        return t
```

- bunch of if문이 보기 싫어서 좀 바꿔주었다.
```python3
from collections import deque
class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        visited = set()
        q = deque()
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == 2:
                    q.appendleft((i,j,0)) # third element is the time orange rottend
        t = 0
        while q:
            i,j,t = q.popleft()
            
            for nr, nc in ((i-1,j), (i+1,j), (i,j-1), (i,j+1)):
                if 0<=nr<len(grid) and 0<=nc<len(grid[0]) and grid[nr][nc] == 1:
                    grid[nr][nc] = 2
                    q.append((nr, nc, t+1))

        
        for i in range(len(grid)):
            if 1 in grid[i]:
                return -1
        
        return t
```

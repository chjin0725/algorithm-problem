# 문제
![leetcode_542](https://user-images.githubusercontent.com/51700219/78038783-376fdf80-73a8-11ea-9d8a-5171ee75bbae.png)
# 풀이
- bfs를 이용하여 풀었다.
- 그러나 원소가 1인 값을 만날때마다 매번 bfs를 해주니 매우 느릴 것이라 생각했다. 실제로 해보니 풀리긴 했으나 매우 느리다.
```python3
from collections import deque
class Solution:
    def updateMatrix(self, matrix: List[List[int]]) -> List[List[int]]:
        # if len(matrix) == 0 or len(matrix[0]) == 0:
        #     return [[]]
        
        ans = [[-1]*len(matrix[0]) for _ in range(len(matrix))]
        
        for row in range(len(matrix)):
            for col in range(len(matrix[0])):
                if matrix[row][col] == 0:
                    ans[row][col] = 0
                else:
                    ans[row][col] = self.bfs(row,col,matrix)
        return ans
    def bfs(self, row, col, matrix):
        q = deque()
        q.append((row,col,0))
        seen = set()
        seen.add((row,col))
        while q:
            r, c, d = q.popleft()
            if matrix[r][c] == 0:
                return d
            else:
                for nr,nc in ((r+1,c), (r-1,c), (r,c+1), (r,c-1)):
                    if 0<=nr<len(matrix) and 0<=nc<len(matrix[0]) and (nr,nc) not in seen:
                        q.append((nr,nc,d+1))
```
# 다른 풀이
- dp로 푸는 방법이다.
- 처음에는 뭔가 dp로 풀어야 할 것 같은 느낌을 받긴 했으나 방법이 떠오르지 않았다.
- dp로 푼다면 예를 들어 (i,j)에서 0까지의 최단거리를 구할 경우 (i-1,j), (i+1,j), (i,j-1), (i,j+1)을 봐야 하는데 i,j를 볼 때 
(i-1,j), (i+1,j), (i,j-1), (i,j+1) 이 4개의 값들이 아직 계산되지 않은 상태일 수 있기 떄문이다.
- 그래서 dp로는 못 푸나 해서 bfs로 풀었다.

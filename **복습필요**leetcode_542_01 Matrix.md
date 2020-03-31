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
- 핵심은 두번 순회하되 처음에는 시작부터 끝 순으로 보고 두번째에서는 끝에서 시작순으로 본다.
- 시작부터 끝까지 볼때는 현재 보고있는 좌표에서 왼쪽과 위쪽중에 더 작은 값에 +1을 한 값을 현재값 으로 한다. 즉 시작점부터 현재값까지 본 값들로 부터 최단거리를 구한다.
- 끝에서 시작까지 볼때는 현재 보고있는 좌표에서 오른쪽과 아래쪽을 본다. 마찬가지로 여기서도 끝점에서 현재값까지 본 값들로부터 최단거리를 구한다. 다만 여기서는 사실상 시작점에서 현재 노드까지 봤을때의 최단거리와 끝점에서 현재노드까지 봤을때의 최단거리를 비교하여 더 짧은 것을 쓰게 된다.
- 이렇게 해도 되는 이유는 시작점에서 현재 노드까지 봤을때의 최단거리와 끝점에서 현재 노드까지 봤을때의 최단거리는 서로 독립이기 때문이다.
- 즉, 시작점부터 현재노드까지 봣을때의 쵣나거리는 끝점에서 현재 노드까지 봤을때의 최단거리가 어떻게 나오든간에 변하지 않기에 이렇게 따로 구해주고 
비교해도 되는 것이다.
```python3
from collections import deque
class Solution:
    def updateMatrix(self, matrix: List[List[int]]) -> List[List[int]]:        
        
        for row in range(len(matrix)):
            for col in range(len(matrix[0])):
                if matrix[row][col] != 0:
                    matrix[row][col] = float('inf')
                    if 0<=row-1 and matrix[row-1][col]+1 < matrix[row][col]:
                        matrix[row][col] = matrix[row-1][col]+1
                    if 0<=col-1 and matrix[row][col-1]+1 < matrix[row][col]:
                        matrix[row][col] = matrix[row][col-1]+1
                    
        for row in range(len(matrix)-1,-1,-1):
            for col in range(len(matrix[0])-1,-1,-1):
                if matrix[row][col] != 0:
                    if row+1<len(matrix) and matrix[row+1][col]+1 < matrix[row][col]:
                        matrix[row][col] = matrix[row+1][col]+1
                    if col+1<len(matrix[0]) and matrix[row][col+1]+1 < matrix[row][col]:
                        matrix[row][col] = matrix[row][col+1]+1
        
        return matrix
```
- 처음보는 형태의 dp이다. 기억해 두자

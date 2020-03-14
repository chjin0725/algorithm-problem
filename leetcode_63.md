# 문제
![leetcode_63](https://user-images.githubusercontent.com/51700219/76677933-ed040a00-6616-11ea-9e75-90a34d6cc2a4.png)

# 풀이
- dp 문제이다.
- 문제에서는 최단거리라고는 언급하지 않았지만 아래 혹은 오른쪽으로만 이동할 수 있으므로 최단거리와 마찬가지이다.
- ans[i][j]가 (i,j)까지 갈수있는 path의 수 일 때 이전 값들로 어떻게 구할 수 있을지를 생각하면 된다.
- 중학교때인가 이런 문제가 수학문제에 많이 있었다. 그게 dp였구나.
- ans[i][j] = ans[i-1][j] + ans[i][j-1] 이다.
- 다만 장애물이 있는 경우를 생각해주어야 한다.
- 먼저 첫 행과 철 열에 장애물이 있을 경우를 생각해야 한다.
- 예를들어  첫 행에 장애물이 있으 경우 그 뒤쪽으로는 갈수있는 방법의 수가 0이다. 그러므로 첫 행의 첫 장애물 이전까지는 값을 1로 하다가
 그 뒤로는 값이 0이 되도록 해야한다.
- 첫 행 혹은 첫 열이 아닌 부분에서 장애물이 있다면 그 부분값을 0으로 해주면 된다.
```python3
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        try:
            num_row = len(obstacleGrid)
            num_col = len(obstacleGrid[0])
        except IndexError as e:
            print(e)
            print('empty list')
        
        if obstacleGrid[-1][-1] == 1 or obstacleGrid[0][0] == 1:
            return 0
        
        flag = False
        for i in range(num_row):
            if obstacleGrid[i][0] == 1 or flag:
                obstacleGrid[i][0] = 0
                flag = True
            else:
                obstacleGrid[i][0] = 1
        
        flag = False
        for j in range(1, num_col):
            if obstacleGrid[0][j] == 1 or flag:
                obstacleGrid[0][j] = 0
                flag = True
            else:
                obstacleGrid[0][j] = 1
        
        for i in range(1, num_row):
            for j in range(1, num_col):
                if obstacleGrid[i][j] == 0:
                    obstacleGrid[i][j] = obstacleGrid[i-1][j] + obstacleGrid[i][j-1]
                else:
                    obstacleGrid[i][j] = 0
        return obstacleGrid[-1][-1]
```
- 중간에 flag는 첫 행 또는 첫 열에서 중간에 1이 나올 경우 그 뒤로는 전부 값을 0으로 해주기 위해 필요하다.
- 근데 풀이를 보니 더 세련된 방법이 있었다.
```python3
for i in range(1,m):
    obstacleGrid[i][0] = int(obstacleGrid[i][0] == 0 and obstacleGrid[i-1][0] == 1)
```
- `and`연산의 결과는 True 혹은 False 이지만 이걸 int로 씌워주면 1 혹은 0으로 바뀐다.

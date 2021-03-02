```python
class Solution:
    def largestSubmatrix(self, matrix: List[List[int]]) -> int:
        
        m = len(matrix)
        n = len(matrix[0])
        
        for i in range(1,m):
            for j in range(n):
                if matrix[i][j] != 0:
                    matrix[i][j] += matrix[i-1][j]
        
        for row in matrix:
            row.sort()
        
        res = 0
        for i in range(m):
            for j in range(n):
                res = max(res, matrix[i][j] * (n-j))
                
        return res
```

  - 열 단위로 인접한 1이 있을 경우 중첩한다.
  - [[0,0,1],[1,1,1],[1,0,1]]이 있다면 이걸 [[0,0,1],[1,1,2],[2,0,3]] 으로 만드는 것임.
  - 그리고 각 행을 sort한 후 행 단위로 각 원소를 보면서 최대값을 갱신한다. 위의 예시의 경우 세번째 행을 sort하면 [0,2,3]이 된다.
  - 이는 인접한 1이 적어도 0개인 열이 3개, 인접한 1이 적어도 2개인 열이 2개, 인접한 1이 적어도 3개인 열이 1개 있다고 이해할 수 있다.
  - 처음에는 막막했는데 a4에 써가면서 한 원소씩 순서대로 보면서 최대값을 갱신하는 dp를 써볼까 하는 식으로 여러 방법을 고민해 보다가 솔루션을 얻게 되었다.
  - 내가 이런 문제를 풀다니 조금 놀랐다. 실력이 조금 오르긴 한 것 같다.

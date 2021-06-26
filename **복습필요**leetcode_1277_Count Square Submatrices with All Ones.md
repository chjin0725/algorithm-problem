
# 풀이
- 처음 봤을때는 dp인지도 몰랐다.
- brute force같은 아이디어 말고는 다른 풀이법이 떠오르지 않았다.
- discuss를 보고 나서야 dp라는걸 알았다.
- 이런 문제들도 많이 풀어봐야 다음에 비슷한 문제를 풀 때 떠올릴 수 있을 것이다.
- 일단 dp[i][j]를 생각해보자. i,j까지 봤을 때의 square의 개수일까?
- 2차 배열일 경우 보통 dp[i][j]를 구하기 전에 dp[i-1][j], dp[i][j-1], dp[i-1][j-1]을 먼저 구한다. 즉 i,j까지 봤다는 건 인덱스가 0~i, 0~j인 dp 값
들을 봤다는 것이다.(0~열의 개수, 0~j 까지 본게아님. 즉 행렬의 각 행을 왼쪽에서 오른쪽으로 순서대로 본게 아님)
- dp[i-1][j], dp[i][j-1], dp[i-1][j-1] 을 알때 dp[i][j]를 어떻게 구할 수 있을지 생각해본다.
- dp[i][j]는 i,j를 오른쪽 아래 원소로 하는 square의 개수이다.
![leetcode_1277_figure](https://user-images.githubusercontent.com/51700219/78384675-94bc9880-7615-11ea-9cae-77f74b4776ed.png)
- 위의 그림을 보면 dp[i][j]는 dp[i-1][j], dp[i][j-1], dp[i-1][j-1] 중에 가장 작은 값 + 1임을 알 수 있다.
```python3
class Solution:
    def countSquares(self, matrix: List[List[int]]) -> int:
        m, n = len(matrix), len(matrix[0])
        for r in range(1, m):
            for c in range(1, n):
                if matrix[r][c] == 1:
                    matrix[r][c] = min(matrix[r-1][c], matrix[r-1][c-1], matrix[r][c-1]) + 1
        
        return sum(map(sum, matrix))
```
- map(sum, matrix)는 matrix의 각 원소(행들)를 sum함수에 넣은 결과를 반환한다. 즉, 각 행의 합들이다. 이걸 한번더 sum하면 매트릭스의 전체 요소의 합을 구할 수 있다.
- 행렬 문제는 대부분 지저분하다고 생각해서 걍 풀기 싫었는데 알고보니 이건 아주 멋진 문제였다.
- 걍 내가  잘 못풀어서 지저분해지는 것도 있다.
- 열심히 연습하자.

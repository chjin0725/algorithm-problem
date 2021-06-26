
# 풀이
- 역시 행렬문제는 머리 아프다.
- 근데 이걸 풀다가 좋은 방법이 떠올랐다.
- 행렬 값들을 왼쪽에서 오른쪽으로 옮기는건 n진법과 같다.(n은 열의 개수)
- 즉, 현재 위치의 열의 인덱스에서 k번 만큼 오른쪽으로 이동했을때 열의 범위를 넘어가면 행의 위치가 +1이 된다.
- 즉, n진법의 첫번째 숫자가 n을 넘어가면 다음숫자가 1만큼 증가하는 것과 같다.
- 이렇게 생각하면 행렬의 값들을 움직이는게 쉽다.
- 나중에 필히 복습해야지

```python3
from itertools import product
class Solution:
    def shiftGrid(self, grid: List[List[int]], k: int) -> List[List[int]]:
        m,n = len(grid), len(grid[0])
        k %= m*n
        
        ans = [[0]*n for _ in range(m)]
        
        for r,c in product(range(m), range(n)):
            shift_row, shift_col = divmod(c+k,n)
            ans[(r+shift_row)%m][shift_col] = grid[r][c]
            
        return ans
```

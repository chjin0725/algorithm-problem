

## 풀이
- inplace로 해야하므로 다른 배열을 쓸 순 없다.
- 처음 돌 때는 자신이 1이면서 주변에 1의 개수가 2개 혹은 3개가 아닐 경우 0으로 바꾸는 대신에 3으로 바꾼다. 즉 3이란 표시는 원래 1인데 다음세대에는 0으로 바뀐 세포이다.
- 마찬가지로 자신이 0이면서 주변에 1의 개수가 3개인 경우 1로 바꾸는 대신 2로 바꾼다. 2는 원래 0인데 1로 바뀐 세포이다.
- 이렇게 한후 두번째 돌때 3은 0으로, 2는 1로 바꿔준다.
```python3
class Solution:
    def gameOfLife(self, board: List[List[int]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        num_r = len(board)
        if num_r == 0:
            return
        num_c = len(board[0])
        if num_c == 0:
            return
        
        
        for r in range(num_r):
            for c in range(num_c):
                num_one = 0
                for nr,nc in ((r-1,c-1), (r-1,c), (r-1,c+1), (r,c-1), (r,c+1), (r+1,c-1), (r+1,c), (r+1,c+1)):
                    if 0<= nr <num_r and 0<= nc <num_c and (board[nr][nc] == 1 or board[nr][nc] == 3):
                        num_one += 1
                
                if board[r][c] == 0 and num_one == 3:
                    board[r][c] = 2
                elif board[r][c] == 1 and (num_one <= 1 or num_one >= 4):
                    board[r][c] = 3
         
        for r in range(num_r):
            for c in range(num_c):
                if board[r][c] == 2:
                    board[r][c] = 1
                elif board[r][c] == 3:
                    board[r][c] = 0
```

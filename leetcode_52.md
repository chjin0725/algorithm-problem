- backtracking 문제.
- reculsion 함수를 잘 이해하고 짜면 어렵지 않게 풀 수 있다.
```python3
class Solution:
    def totalNQueens(self, n: int) -> int:
        pos_queens = []
        return self.backtrack(0, 0, n, pos_queens)
        
    def backtrack(self, row, count, n, pos_queens):
        for col in range(n):
            if self.not_under_attack(row, col, pos_queens):
                pos_queens.append([row, col]) # place a queen.
                
                if row + 1 == n:
                    count += 1
                
                else:
                    count = self.backtrack(row+1, count, n, pos_queens)
                
                pos_queens.pop() # remove a queen
        
        return count
    
    def not_under_attack(self, row, col, pos_queens):
        for r,c in pos_queens:
            if c == col:
                return False
            if r+c == row+col:
                return False
            if (r-c) == (row-col):
                return False
        
        return True
```

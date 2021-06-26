
# 풀이
- 각 row의 최소값을 찾은 다음 그 값의 열을 확인한다.
- 열에서 해당 값보다 큰게 없으면 answer에 추가.
```python3
class Solution:
    def luckyNumbers (self, matrix: List[List[int]]) -> List[int]:
        m, n = len(matrix), len(matrix[0])
        answer = []
        temp = []
        for row in range(m):            
            temp.append((row,matrix[row].index(min(matrix[row]))))
        
        for row, col in temp:
            target = matrix[row][col]
            flag = True
            for r in range(m):
                if matrix[r][col] > target:
                    flag = False
                    break
            if flag:
                    answer.append(target)
        
        return answer
```

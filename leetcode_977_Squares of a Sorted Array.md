# 문제
![leetcode_977](https://user-images.githubusercontent.com/51700219/79356288-b99bfe80-7f79-11ea-96d1-2bc316a6dfdb.png)
# 풀이
- 배열의 왼쪽 끝과 오른쪽 끝부터 보면서 절대값이 큰 값을 answer배열에 차례대로 넣어준다.
```python3
class Solution:
    def sortedSquares(self, A: List[int]) -> List[int]:
        l = 0
        h = index = len(A) - 1
        answer = [0]*len(A)
        
        while l <= h:
            if abs(A[l]) < abs(A[h]):
                answer[index] = A[h]**2
                h -= 1
                index -= 1
            else:
                answer[index] = A[l]**2
                l += 1
                index -= 1
        
        return answer
```

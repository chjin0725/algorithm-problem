# 문제
![leetcode_1005](https://user-images.githubusercontent.com/51700219/77720798-4a8f5200-702c-11ea-81f5-4070b29d282c.png)

# 풀이
- A에서 가장 최소값을 계속 뽑아서 -1을 곱해주면 되는 greedy 문제이다.
- 최소값을 계속 뽑으므로 heapq가 적절한 자료구조가 될 수 있다.
```python3
import heapq
class Solution:
    def largestSumAfterKNegations(self, A: List[int], K: int) -> int:
        if not A:
            return 0
        heapq.heapify(A)
        for _ in range(K):
            min_value = heapq.heappop(A)
            heapq.heappush(A, -min_value)
        
        return sum(A)
```

# 다른 풀이
- 정렬을 이용할 수 도 있다.
```python3
class Solution:
    def largestSumAfterKNegations(self, A: List[int], K: int) -> int:
        if not A:
            return 0
        A.sort()
        i = 0
        while i < K and A[i] < 0:
            A[i] = -A[i]
            i += 1
        if i < K:
            min_index = i if A[i] <= A[i-1] else (i-1)
            if (K-i)%2 == 1:
                A[min_index] = (-1)*A[min_index]
            
        
        return sum(A)
```

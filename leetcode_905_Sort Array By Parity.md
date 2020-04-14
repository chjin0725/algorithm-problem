# 문제
![leetcode_905](https://user-images.githubusercontent.com/51700219/79239630-c05c4000-7eab-11ea-8e8f-81adeffa0315.png)
# 풀이
- 새로운 배열을 A와 같은 길이로 초기화하고 루프 돌면서 짝수가 나오면 새로운 배열의 첫부분부터 넣고 홀수가 나오면 끝부분 부터 넣는다.
- 넣어준 인덱스를 계속 기록하면서 하면 됨
- in place로 하면 조금 더 복잡하다.
- 일단 먼저 맨 처음 나오는 홀수의 인덱스를 알아낸 후,
- 알아낸 홀수 인덱스 다음부터는 짝수가 나오면 홀수의 인덱스와 스왑하고 인덱스를 1만큼 증가 시킨다.
```python3
class Solution:
    def sortArrayByParity(self, A: List[int]) -> List[int]:
        n = l = len(A)
        for i in range(n):
            if A[i]%2 != 0:
                l = i
                break
        for i in range(l+1,n):
            if A[i]%2 == 0:
                temp = A[i]
                A[i] = A[l]
                A[l] = temp
                l += 1
        return A
```

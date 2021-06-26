

# 풀이
- 행렬다루는 문제는 특히 코드가 지저분해진다.
- 다른문제에서도 마찬가지겠지만 행렬 다룰때는 특히 코드의 가독성에 신경쓰자.
- 최대한 읽기 좋으면서 간결하게 쓴다.
- discuss에서 다른사람의 간결한 코드 배끼기.
- 행렬 다룰때는 먼저 m,n에 행의 개수, 열의 개수를 담고 len()이 필요할 때 대신 쓴다. len()을 자주쓰면 보기 안좋음.
```python3
class Solution:
    def matrixScore(self, A: List[List[int]]) -> int:
        m,n = len(A), len(A[0])
        
        ans = (1<<n-1)*m
        
        for c in range(1,n):
            num_one_in_column = sum(A[r][c] == A[r][0] for r in range(m))
            ans += (1<<n-c-1)*max(num_one_in_column, m-num_one_in_column)
        
        return ans
```
- 이 코드는 어떻게 풀지 알아내고 나서 구현을 어떻게 할지를 보려고 discuss를 보고 배낀 것이다.
- 먼저 각 행의 첫번째 값은 무조건 1인게 좋으므로 첫번쨰 값이 0인 행은 무조건 토글한다.
- 그 다음 값들은 열마다 본다. 각 열에서 1의 개수가 (전체열의 개수//2)보다 적으면 그 열은 토글한다.
- 행렬 요소값을 바꾸지도 않고 풀 수 있는거였음.
- 행렬문제는 코드가 지저분해서 풀기 싫어지는데 이런식으로 간결하게 표현하려고 하면 재밌을 듯.
- 파이썬에서는 ``sum(A[r][c] == A[r][0] for r in range(m))``와 같이 for문을 한 줄로 표현할 수 있으므로 더 간결하다. 이것도 애용하기!!

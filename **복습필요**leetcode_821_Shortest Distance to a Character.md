# 문제
![leetcode_821](https://user-images.githubusercontent.com/51700219/79681967-72ec2400-8259-11ea-958a-0f149cf41b53.png)
# 풀이
- 처음에는 왼쪽에서 오른쪽으로 가면서 C가 나오면 거리를 0으로 하고 C가 아니면 바로 이전 인덱스+1과 비교하여 더 작은 것을 쓴다.
- 두번째에서는 처음과 같지만 오른쪽에서 왼쪽으로 확인한다.
- 이런식으로 한번은 오른쪽 방향으로, 다음번엔 왼쪽 방향으로 돌면서 확인하는 방식이 종종 쓰인다. 기억해두기
```python3
class Solution:
    def shortestToChar(self, S: str, C: str) -> List[int]:
        n = len(S)
        ans = [10000]*n
        
        ans[0] = 0 if S[0] == C else 10000
        
        for i in range(1, n):
            if S[i] == C:
                ans[i] = 0
            else:
                ans[i] = min(ans[i], ans[i-1]+1)
                
        for i in range(n-2, -1, -1):
            if S[i] == C:
                ans[i] = 0
            else:
                ans[i] = min(ans[i], ans[i+1]+1)
        
        return ans
```

- 더 간결한 코드
```python3
def shortestToChar(self, S, C):
        n = len(S)
        res = [0 if c == C else n for c in S]
        for i in range(1, n):
            res[i] = min(res[i], res[i - 1] + 1)
        for i in range(n - 2, -1, -1):
            res[i] = min(res[i], res[i + 1] + 1)
        return res
```

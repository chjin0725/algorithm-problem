- 문제 링크: https://leetcode.com/problems/minimum-difficulty-of-a-job-schedule/
- dp문제 이다. 최소, 최대 이런거 나오면 거의 dp라고 봐도 될 것 같다.
- state variable은 2개이다. day와 배열의 index.
- 이 문제는 하나의 dp[d][i] 값을 구할 때 최대 n번의 iteration이 추가로 필요하다.


```python3
class Solution:
    def minDifficulty(self, jobDifficulty: List[int], d: int) -> int:
        n = len(jobDifficulty)
        if n < d:
            return -1
        
        pre_row = [0]*(n-d+1)
        
        max_diffi = -1
        for i in range(n-d+1):
            max_diffi = max(max_diffi, jobDifficulty[i])
            pre_row[i] = max_diffi
        
        for cur_d in range(1, d):
            temp = [float('inf')]*(n-d+1)
            
            for i in range(n-d+1):
                max_diffi = -1
                
                for j in range(i, -1, -1):
                    max_diffi = max(max_diffi, jobDifficulty[cur_d+j])
                    temp[i] = min(temp[i], pre_row[j] + max_diffi)
            pre_row = temp
        
        return pre_row[-1]
```

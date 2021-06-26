

# 풀이
- 그냥 감으로 푼 것 같다. 문제유형은 모르겠다
- 서로 위치차이가 짝수만큼 나는 칩들은 코스트 없이 한자리로 모을 수 있다.
- 이런식으로 서로 홀수만큼 차이나는 두 위치에 모든 칩을 cost없이 모은 다음 두 위치 중 개수가 더 작은 것을 남은 위치로 옮기면 된다.
```python3
class Solution:
    def minCostToMoveChips(self, chips: List[int]) -> int:
        if len(chips) == 0 or len(chips) == 1:
            return 0
        first_pos = chips[0]
        
        num_first_pos = 0
        num_sec_pos = 0
        
        for pos in chips:
            if abs(first_pos - pos)%2 == 0:
                num_first_pos += 1
            else:
                num_sec_pos += 1
                
        return min(num_first_pos, num_sec_pos)
```

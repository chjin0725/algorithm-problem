

# 풀이
- 그리디 문제
- 문자열을 두번 순회하는데
- 첫 순회에서는 각 문자가 마지막으로 나온 index를 알아낸다.
- 두번째 순회에서 파티션을 진행하는데 방법은 다음과 같다.
- 첫 시작점을 0으로 하고 0에 해당하는 문자의 마지막 index를 확인한다. 이를 end라 하자
- 문자열를 순회하면서 각 문자의 마지막 index가 end보다 크면 end를 이 값으로 갱신해준다.
- 각 문자를 계속 보다가 현재 문자의 index가 end와 같으면 여기서 끊어준다.
- 즉 각 문자의 시작index와 마지막으로 등장하는 index의 합집합을 구하는 것이다.
```python3
class Solution:
    def partitionLabels(self, S: str) -> List[int]:
        
        temp = 0
        ans = []
        
        end_pos = dict()
        for i in range(len(S)):
            if S[i] not in end_pos:
                end_pos[S[i]] = i
            else:
                end_pos[S[i]] = i
        
        start = 0
        end = 0
        for i in range(len(S)):
            if end_pos[S[i]] > end:
                end = end_pos[S[i]]
            elif i == end:
                ans.append(end - start +1)
                start = i+1
                end = i+1
        
        return ans
```

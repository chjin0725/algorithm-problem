# 문제
![leetcode_1337_1](https://user-images.githubusercontent.com/51700219/76525298-f1adae80-64ae-11ea-833a-fba62cc244eb.png)
![leetcode_1337_2](https://user-images.githubusercontent.com/51700219/76525315-fd00da00-64ae-11ea-9776-4d22076c607c.png)

# 풀이 
```python
class Solution:
    def kWeakestRows(self, mat: List[List[int]], k: int) -> List[int]:
        ans = []
        seen = set()
        for col in range(len(mat[0])):
            for row in range(len(mat)):
                if row not in seen and mat[row][col] == 0:
                    ans.append(row)
                    seen.add(row)
                    if len(ans) == k:
                        return ans
```
- 각 열에 대하여 행을 돌면서 0인게 있으면 추가해주는 식으로 하였다.
- 이렇게 했더니 입력이 `[[1,1,1,1,1,1],[1,1,1,1,1,1],[1,1,1,1,1,1]]` 이런 입력에 대해서는 풀지 못하였다.
- 이런 입력에는 0이 아예 없는 케이스 이니 안풀리는게 당연하다.
```python
class Solution:
    def kWeakestRows(self, mat: List[List[int]], k: int) -> List[int]:
        ans = []
        seen = set()
        for col in range(len(mat[0])):
            for row in range(len(mat)):
                if row not in seen and mat[row][col] == 0:
                    ans.append(row)
                    if len(ans) == k:
                        return ans
                    seen.add(row)
        
        for row in range(len(mat)):
            if row not in seen:
                ans.append(row)
                if len(ans) == k:
                    return ans
                seen.add(row)
```
- 이런식으로 예외케이스도 다룰 수 있게 하였다.
- 처음에 코드를 구현할 때 test case에 대한 생각 없이 구현하여 이런 실수를 저지른것 같다.
- 항상 테스트케이스에 대해서 먼저 고민해보고 구현해야 한다.
- 시간복잡도 o(mk) 공간복잡도 o(k)
- 정렬되있다고 볼 수 있으므로 각 행에서 처음으로 0이 시작하는 인덱스가 작은 순으로 ans.append할 수도 있겠다. 이러면 시간복잡도는 mlogn일 듯.
- 이전에 1351번에서 구현한 바이너리 서치를 그대로 이용할 수 있을 듯.

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
# 다른 풀이
- 마침 누군가가 바이너리 서치로 구현을 해놨다.
```python
from heapq import nsmallest

class Solution:
  def kWeakestRows(self, mat: List[List[int]], k: int) -> List[int]:
    return [i for count, i in nsmallest(k, ((self.count_ones(row), i) for i, row in enumerate(mat)))]

  def count_ones(self, a):
    x, lo, hi = 0, 0, len(a)
    while lo < hi:
      mid = (lo+hi)//2
      if a[mid] > x: lo = mid+1
      else: hi = mid
    return lo
```
- heapq는 이진트리 기반의 최소 힙 자료구조이다. 프라이오리티큐 라고 보면 된다. 참고로 최대힙은 따로 없지만 heapq를 요령껏 쓰면 구현할 수는 있다. 이건 인터넷 검색해보기
- nsamllest는 주어진 iterable 자료형에서 제일 작은것 n개를 정렬해서 리스트로 반환해준다.
- 시간 복잡도는 mlogn + mlogk라고 하는데 잘 이해 안된다. 위 쪽에 return하는 부분이 이해가 잘 안된다. 파이썬에서는 line 하나로만 저렇게 적을수는 있지만 가독성은 매우 별로인것 같다. 따라하지 말아야지

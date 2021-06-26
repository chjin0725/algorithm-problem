

# 풀이
- 정렬이 되어있으면 바이너리 서치를 떠올려보자.
- 정렬된 상태이므로 각 행에 대하여 -1 이하인 숫자의 인덱스를 바이너리서치로 찾아주면 된다.

~~~python
def binary_search_descending(list, value):
  lo = 0
  hi = len(list)-1
  mid = (lo+hi)//2
  
  while lo <= hi:

    if list[mid] == value:
      while list[mid-1] == value:
        mid -= 1
      return mid
    elif list[mid] > value:
      lo = mid+1
      mid = (lo+hi)//2
    else:
      hi = mid-1
      mid = (lo+hi)//2
  
  return -1
~~~

- 위 코드에서 `mid = (lo+hi)//2` 를 두번 하므로 보기 안좋다. while문 시작 부분으로 옮겨주자.
~~~python
def binary_search_descending(list, value):
  lo = 0
  hi = len(list)-1
  mid = (lo+hi)//2
  
  while lo <= hi:
    mid = (lo+hi)//2
    if list[mid] == value:
      while list[mid-1] == value:
        mid -= 1
      return mid
    elif list[mid] > value:
      lo = mid+1
    else:
      hi = mid-1
  
  return -1
~~~
- 여기서 문제가 있는데
  - 첫번째로 [1, -1, -1, -1, -1] 같은 경우에는 1을 반환해줘야 하는데 2를 반환해준다.
  - 두번째로 [1, 0, -3, -4, -4] 같은 경우에는 2 반환해줘야하는데 -1을 찾지 못해서 -1을 반환한다.
  - 파이썬의 bisect 처럼 최초로 조건을 만족하는 부분을 찾아 주도록 바꿀 필요가 있음.
- 파이썬의 bisect_left의 소스코드를 살펴보자.
~~~python
def bisect_left(a, x, lo=0, hi=None):
    """Return the index where to insert item x in list a, assuming a is sorted.
    The return value i is such that all e in a[:i] have e < x, and all e in
    a[i:] have e >= x.  So if x already appears in the list, a.insert(x) will
    insert just before the leftmost x already there.
    Optional args lo (default 0) and hi (default len(a)) bound the
    slice of a to be searched.
    """

    if lo < 0:
        raise ValueError('lo must be non-negative')
    if hi is None:
        hi = len(a)
    while lo < hi:
        mid = (lo+hi)//2
        if a[mid] < x: lo = mid+1
        else: hi = mid
    return lo
~~~
- 여기서는 x값이 있으면 최초의 x의 위치를, x가 없으면 x가 들어갈 자리를 찾아주기 떄문에 `if a[mid] == x`와 같은 부분은 없다.
- x값이 있으면 최초의 x의 위치를, x가 없으면 x가 들어갈 자리를 찾기 위해서는 x이상인 최초의 숫자를 찾아야 한다.
- 바이너리 서치에서 lo와 hi는 탐색 범위라고 생각하면 된다. 여기서는 lo ~ hi-1을 탐색범위로 정하고 있다.
- `a[mid] < x`인 경우는 lo ~ mid 까지는 전부 x보다 작기 때문에 볼 필요 없다. 그래서 lo = mid+1을 해주는 것이다.
- 마찬가지로 `a[mid] >= x`인 경우는 mid 에서 hi 까지는 볼 필요가 없다.(물론 mid가 x일 수 있지만 최초의 x인지 확인해야 하므로 lo ~ mid-1까지 봐야한다. mid부터는 볼 필요 없음) 그래서 hi = mid로 해준다.
- lo == high 인 경우는 볼 필요가 없기 때문에 lo < hi로 조건을 걸어준다( lo != hi로 하면 list의 크기가 1인 경우는 처리할 수 없으므로 lo < hi로 한다)
- lo == high가 되기 바로 전 단계를 생각해보자. 탐색범위에 숫자는 두개가 남아 있는 상태에서 하나의 숫자는 lo이자 mid이고 다른 남은 숫자가 hi일 것이다. 이때 a[mid] < x 인 경우와 그렇지 않은 경우를 생각해보자. 두 경우 모두에서 lo == high가 되는 경우까지 계산해 줄 필요가 없음을 알 수 있다.
- 파이썬의 bisect는 x가 발견되어도 lo < hi 를 만족하지 않을 때까지 계속 while문을 돈다. 그러므로 워스트케이스를 따질 필요 없이 어떤 리스트를 쓰든 시간은 nlogn만큼 걸릴 것이다.(이건 내 생각임)
~~~python
def bisect_left(a, x, lo=0, hi=None):


    if lo < 0:
        raise ValueError('lo must be non-negative')
    if hi is None:
        hi = len(a)
    while lo <= hi:
        mid = (lo+hi)//2
        if a[mid] < x: lo = mid+1
        else: hi = mid-1
    return lo
~~~
- 탐색범위를 lo ~ hi로 생각한다면 위와 같이 구현하면 된다. while의 조건부분과 hi를 
~~~python
    def binary_search_descending(self, l, value):
        lo = 0
        hi = len(l)
        mid = (lo+hi)//2

        while lo < hi:
            mid = (lo+hi)//2
            if l[mid] > value:
                lo = mid+1
            else:
                hi = mid


        return lo
~~~
- 이렇게 하면 내림차순에 대해서 같은 기능을 구현할 수 있다.
- 최종 코드는 아래와 같다.
~~~python
class Solution:
    def countNegatives(self, grid: List[List[int]]) -> int:
        if len(grid) == 0 or len(grid[0]) == 0:
            return 0
        ans = 0
        n = len(grid[0])
        for row in grid:
            idx_of_minus1 = self.binary_search_descending(row,-1)
            ans += (n-idx_of_minus1)
        
        return ans
            
    def binary_search_descending(self, l, value):
        lo = 0
        hi = len(l)
        mid = (lo+hi)//2

        while lo < hi:
            mid = (lo+hi)//2
            if l[mid] > value:
                lo = mid+1
            else:
                hi = mid


        return lo
~~~
- 시간복잡도는 mlgn
# 다른풀이
- 오른쪽 대각선 맨 위의 숫자부터 시작해서
  - 현재 보고있는 숫자가 음수면 그 아래로는 전부 음수이므로 이걸 카운팅하고 왼쪽숫자를 확인한다.
  - 현재 보고있는 숫자가 양수면 아래의 숫자를 확인한다.
- 이건 시간복잡도가 m+n이므로 경우에 따라서 더 빠를 수 있겠다.
- 구현은 다음과 같다.
```python
class Solution:
    def countNegatives(self, grid: List[List[int]]) -> int:

        ans = 0
        num_row = len(grid)
        row = 0
        col = len(grid[0]) - 1
        while row < num_row and col >= 0:
            if grid[row][col] < 0:
                ans += (num_row - row)
                col -= 1
            else:
                row += 1
        return ans
 ```

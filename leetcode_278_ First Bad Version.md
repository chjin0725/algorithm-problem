# 문제 
![leetcode_257](https://user-images.githubusercontent.com/51700219/77531631-9203ca00-6ed6-11ea-8ce4-e28452509ff5.png)

# 풀이
- 이진 탐색을 사용한다.
```python3
class Solution:
    def firstBadVersion(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n == 1 or isBadVersion(1):
            return 1
        lo = 1
        hi = n
        
        while lo <= hi:
            mid = (lo + hi)//2
            if isBadVersion(mid):
                if not isBadVersion(mid-1):
                    return mid
                else:
                    hi = mid-1
            else:
                lo = mid+1
```
- `if not isBadVersion(mid-1):` 이 부분을 하는 이유는 mid가 첫 bad version인지를 확인하기 위해서 이다. 바로 왼쪽것이 bad version이 아닐 경우
mid가 답이다.
- 그러나 잘 보면 이건 파이썬의 bisect와 비슷하다. 맨 첫번쨰의 것을 찾아주고 있기 때문이다.
# bisect 알고리즘을 이용한 풀이
```python3
class Solution:
    def firstBadVersion(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n == 1 or isBadVersion(1):
            return 1
        lo = 1
        hi = n
        
        while lo <= hi:
            mid = (lo + hi)//2
            if isBadVersion(mid):
                hi = mid-1
            else:
                lo = mid+1
                
        return lo
```
- bisect를 이용할 때는 mid가 아니라 lo를 리턴해준다. 
- 원래 이진 탐색은 찾았으면 mid를 리턴하는 식인데 bisect는 찾는다고 끝이 아니라 원소가 중복으로 있을 경우 가장 첫번째 것을 찾아주기 때문에
lo를 리턴해주는 것이다. mid는 리턴하지 않는다.
- while문을 만족하지 않을때 까지 while문을 돌다보면 찾는 것이 잇을 경우 lo는 찾는것이 맨 처음으로 나온 인덱스를, 찾는것이 없을 경우 lo는 찾는것이
들어가야할 위치를 반환한다.
- 이건 걍 외워 두는게 좋을 듯. 간혹 쓸모가 있음.

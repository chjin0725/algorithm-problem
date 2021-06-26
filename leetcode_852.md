

# 풀이
peak을 기준으로 왼쪽 오른쪽 모두 정렬되어 있다. 정렬되어 있으면 이진탐색을 생각해볼 수 있다.
~~~python3
class Solution:
    def peakIndexInMountainArray(self, A: List[int]) -> int:
        lo = 1
        hi = len(A) - 2
        
        while True:
            mid = (lo+hi)//2
            if A[mid-1] < A[mid] < A[mid+1]:
                lo = mid + 1
            elif A[mid-1] > A[mid] > A[mid+1]:
                hi = mid - 1
            else:
                return mid
~~~

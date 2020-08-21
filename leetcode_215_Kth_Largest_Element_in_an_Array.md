# 문제
![20200821_214725](https://user-images.githubusercontent.com/51700219/90892227-f41a1a00-e3f7-11ea-8ed1-df2f65b2e4f2.png)


# 풀이
 - heapq를 쓴다. heapq는 min heap으로 되어있으므로 nums의 값들에 -를 붙여준다.
 ```python3
 import heapq
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        for i in range(len(nums)):
            nums[i] = -nums[i]
        heapq.heapify(nums)
        
        for _ in range(k-1):
            heapq.heappop(nums)
        
        return -heapq.heappop(nums)
 ```

- 이진탐색 문제이다.
- 그리 어렵진 않다. 다만 이진탐색 알고리즘의 lo,hi와 종료조건을 잘 생각해야함.
- test case를 직접 만들어서 손으로 쓰면서 해보면 어렵지 않게 알 수 있다.
- 실행하기전에 런타임에러 없을지 확인하고 edge case나 다른 case들 먼저 생각해보고 실행하자.
- 에러없는 코드를 바로 짤 수 있어야 함.
```python3
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        ans = [-1,-1]
        
        lo = 0
        hi = len(nums)-1
        flag = True
        while lo <= hi and flag:
            mid = lo + (hi-lo)//2
            
            if nums[mid] > target:
                hi = mid - 1
                
            elif nums[mid] < target:
                lo = mid + 1
            
            else:
                flag = False
                ans[0] = self.search_left(lo, mid, target, nums)
                ans[1] = self.search_right(mid, hi, target, nums)
            
        return ans
    
    def search_left(self, lo, hi, target, nums):
        while lo <= hi:
            mid = lo + (hi-lo)//2
            if nums[mid] < target: # lo는 target이 아니거나 target의 첫번째 인덱스거나 둘중 하나이다.
                lo = mid+1   # lo가 target의 첫번쨰 인덱스가 되는 순간 lo는 고정이고 hi만 계속 작아진다.
                             # 그래서 lo == hi가 되면 lo를 return하는 것임.
            else: # nums[mid] == target일 경우
                hi = mid-1
        
        return lo
    
    def search_right(self, lo, hi, target, nums):
        while lo <= hi:
            mid = lo + (hi-lo)//2
            if nums[mid] > target:
                hi = mid-1
            else: # nums[mid] == target 일 경우
                lo = mid+1
        
        return hi
```

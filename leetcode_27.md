- 주어진 배열에서 특정 원소를 전부 제거하고 남은 원소들을 맨 앞으로 당겨놓으면 된다.
- 스왑만 잘 하면 어렵지 않게 풀 수 있다.
```python3
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        
        num_val = 0
        for n in nums:
            num_val += (n == val)
        
        i = 0
        j = len(nums) - 1
        while i < len(nums) - num_val:
            while nums[i] == val:
                temp = nums[j]
                nums[j] = nums[i]
                nums[i] = temp
                j -= 1
            
            i += 1
        
        return len(nums) - num_val
```

# 문제
![leetcode_303](https://user-images.githubusercontent.com/51700219/77822592-97138400-7137-11ea-9573-fa799f4ff7f6.png)

# 풀이
- init을 최대한 빠르게 하고 query를 o(1)으로 맞춰야 한다.
```python3
class NumArray:

    def __init__(self, nums: List[int]):
        for i in range(1, len(nums)):
            nums[i] = nums[i-1] + nums[i]
        self.sums = nums
            
    def sumRange(self, i: int, j: int) -> int:
        if i == 0:
            return self.sums[j]
        else:
            return self.sums[j] - self.sums[i-1]

# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(i,j)
```

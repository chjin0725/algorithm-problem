# 문제
![leetcode_283](https://user-images.githubusercontent.com/51700219/78450647-16b2cd00-76bb-11ea-93e1-b0326645dd9c.png)
# 풀이
- two pointer 문제이다.
- 먼저 제일 왼쪽의 0의 위치를  찾은 후 그 위치부터 순회를 시작하여 0이 아닌 값을 만나면 제일 왼쪽의 0과 바꿔준다.
```python3
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        first_zero = -1
        for i in range(len(nums)):
            if nums[i] == 0:
                first_zero = i
                break
        if first_zero == -1:
            return
        j = first_zero
        for i in range(first_zero, len(nums)):
            if nums[i] != 0:
                temp = nums[j]
                nums[j] = nums[i]
                nums[i] = temp
                j += 1

```

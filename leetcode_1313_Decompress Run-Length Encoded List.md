
# 풀이
- 지금 이 문제를 깃허브에 적고있는 시간이 아까울 정도로 너무 쉬운 문제
```python3
class Solution:
    def decompressRLElist(self, nums: List[int]) -> List[int]:
        ans = []
        for i in range(len(nums)//2):                        
            for _ in range(nums[2*i]):
                ans.append(nums[2*i+1])
                
        return ans
```

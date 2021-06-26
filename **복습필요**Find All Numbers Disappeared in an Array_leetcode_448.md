

# 풀이
- 자신에 위치에 있지 않은 숫자가 나오면 자신의 위치로 스왑해준다.
- 현재위치에 있어야할 숫자가 있을때까지 혹은 스왑하려는 숫자가 현재위치의 숫자와 같을때(중복된 숫자)까지 스왑해준다.
- 이런식으로 한번 순회하면 중복된 숫자들을 제외하고는 모든 숫자는 자신의 위치에 있게 된다.
```python3
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        
        for i in range(len(nums)):
            while i+1 != nums[i]:
                if nums[nums[i]-1] != nums[i]:
                    
                    temp = nums[i]
                    nums[i] = nums[temp-1]
                    nums[temp-1] = temp
                else:
                    break
        
        ans = []
        for i in range(len(nums)):
            if i+1 != nums[i]:
                ans.append(i+1)
        return ans
```

# 다른 풀이
- 스왑하지 않고 마커를 둔다.
```java
public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> res = new ArrayList<>();
        int n = nums.length;
        for (int i = 0; i < nums.length; i ++) nums[(nums[i]-1) % n] += n;
        for (int i = 0; i < nums.length; i ++) if (nums[i] <= n) res.add(i+1);
        return res;
    }
```

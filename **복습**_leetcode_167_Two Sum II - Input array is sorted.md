## 문제
![leetcode_167](https://user-images.githubusercontent.com/51700219/84157032-2e387880-aaa5-11ea-84bc-dc6c0dbb5cf1.png)

## 풀이
- 이분탐색을 해준다.
- 다만 [0,0,3,4], target=0 인 경우도 있으므로 탐색범위를 현재 보고있는 인덱스+1 부터 끝까지로 한다.
- 코드에서는 이부분을 offset으로 구현함.
```python3
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        
        for i in range(len(numbers)):
            find = target - numbers[i]
            
            result = self.bs(find, numbers, i)
            if result != -1 and result != i:
                answer = [i+1, result+1]
                return answer
        
    def bs(self, t, array, offset):
        lo = offset+1
        hi = len(array)
        
        while lo < hi:
            mid = (lo + hi)//2
            if array[mid] > t:
                hi = mid
            elif array[mid] < t:
                lo = mid + 1
            else:
                return mid
        return -1
```

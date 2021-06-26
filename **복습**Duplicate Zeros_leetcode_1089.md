
# 풀이
- 먼저 arr 안에 0의 개수를 세어 준다.
- 그 다음 arr의 맨 뒤에서부터 순회하면서 각 요소를 옮겨준다. 0의 개수를 알고 있으므로 최종적으로 각 요소가 어디에 배치될지를 알 수 있다.
- 배열을 거꾸로 순회하는 것은 자주 사용되는 트릭이다. 기억해두기.
```python3
class Solution:
    def duplicateZeros(self, arr: List[int]) -> None:
        """
        Do not return anything, modify arr in-place instead.
        """
        num_zero = 0
        for n in arr:
            if n==0:
                num_zero += 1
        l = len(arr)
        for i in range(l-1, -1, -1):
            if num_zero == 0:
                break
            
            if i + num_zero < l:
                arr[i+num_zero] = arr[i]
                
                    
            if arr[i] == 0:
                num_zero -= 1
                if i + num_zero < l:
                    arr[i + num_zero] = 0
```

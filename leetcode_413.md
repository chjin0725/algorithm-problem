```python
class Solution:
    def numberOfArithmeticSlices(self, A: List[int]) -> int:
        '''count number of aritnmetic slices
        
        Example: 
        >>> numberOfArithmeticSlices([1,3,5,7,9])
        10
        >>> numberOfArithmeticSlices([1,1,2,3,6])
        1
        
        Args:
            A (list): int list
        
        Return:
            int : number of aritnmetic slices
        '''
        if len(A) < 3:
            return 0
        
        ans = 0
        pre = A[1] - A[0]
        num_same_diff = 1
        for i in range(2, len(A)):
            cur = A[i] - A[i-1]
            if cur == pre:
                num_same_diff += 1
            
            else:
                ans += num_same_diff*(num_same_diff-1)/2
                pre = cur
                num_same_diff = 1
        ans += num_same_diff*(num_same_diff-1)/2 
            
        
        return int(ans)
```

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort(key = lambda x : x[0])
        
        res = []
        start, end = intervals[0]
        for i in range(1, len(intervals)):
            start_next, end_next = intervals[i]
            
            if end >= start_next:
                end = max(end, end_next)
            
            else:
                res.append([start, end])
                start = start_next
                end = end_next
        
        res.append([start, end])
        
        return res
```

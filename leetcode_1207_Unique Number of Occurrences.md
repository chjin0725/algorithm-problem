
# 풀이
- 해쉬 이용하면 간단히 풀림
```python3
from collections import defaultdict
class Solution:
    def uniqueOccurrences(self, arr: List[int]) -> bool:
        num_occur = defaultdict(lambda : 0)
        for n in arr:
            num_occur[n] += 1
        
        num_unique = len(num_occur)
        
        return num_unique == len(set(num_occur.values()))
```

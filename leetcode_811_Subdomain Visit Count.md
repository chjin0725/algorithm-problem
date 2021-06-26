
# 풀이
- 딕셔너리 이용해서 세어주면 됨
```python3
from collections import defaultdict
class Solution:
    def subdomainVisits(self, cpdomains: List[str]) -> List[str]:
        num_visit = defaultdict(lambda : 0)
        for s in cpdomains:
            split_space = s.split(' ')
            num_visit[split_space[1]] += int(split_space[0])
            split_dot = split_space[1].split('.')
            
             
            num_visit[split_dot[-1]] += int(split_space[0])
            if len(split_dot) > 2:
                num_visit[split_dot[-2] + '.' + split_dot[-1]] += int(split_space[0])
        
        ans = []
        for key, val in num_visit.items():
            ans.append(str(val) + ' ' + key)
        
        return ans
```

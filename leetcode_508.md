```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import defaultdict
class Solution:
    def findFrequentTreeSum(self, root: TreeNode) -> List[int]:
        self.d = defaultdict(int)
        
        def sum(node):
            if node == None:
                return 0
            res = sum(node.left) + sum(node.right) + node.val
            
            self.d[res] += 1
            
            return res
        
        sum(root)
        
        output = []
        max_occur = 0
        for v in self.d.values():
            max_occur = max(max_occur, v)
        
        for k, v in self.d.items():
            if v == max_occur:
                output.append(k)
        
        return output
```

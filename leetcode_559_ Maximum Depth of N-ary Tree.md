

# 풀이
- lever order traversal로 푼다.
```python3
class Solution:
    def maxDepth(self, root: 'Node') -> int:
        if root is None:
            return 0
        parent = [root]
        d = 0
        while parent:
            children = []
            d += 1
            for node in parent:
                for child in node.children:
                    children.append(child)
            parent = children
        
        return d
        
```

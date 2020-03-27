# 문제
![leetcode_559](https://user-images.githubusercontent.com/51700219/77742620-16328a80-705a-11ea-9225-c059ed8c1847.png)

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

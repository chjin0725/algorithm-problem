# 문제
![leetcode_111](https://user-images.githubusercontent.com/51700219/77746449-4bda7200-7060-11ea-9b41-9f4d6fb03514.png)
# 풀이
- level order traversal로 푼다.
- child가 없는 노드를 만나면 바로 depth를 리턴하도록 한다.
```python3
class Solution:
    def minDepth(self, root: TreeNode) -> int:
        if root is None:
            return 0
        
        parent = [root]
        d = 0
        while parent:
            child = []
            d += 1
            for node in parent:
                if node.left is None and node.right is None:
                    return d
                else:
                    if node.left is not None:
                        child.append(node.left)
                    if node.right is not None:
                        child.append(node.right)
            
            parent = child
```

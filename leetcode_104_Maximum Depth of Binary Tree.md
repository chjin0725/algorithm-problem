# 문제
![leetcode_104](https://user-images.githubusercontent.com/51700219/77741181-d10d5900-7057-11ea-813d-519ee5179005.png)

# 풀이
- level order traversal 로 풀면 된다.
```python3
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        if root is None:
            return 0
        parent = [root]
        d = 0
        while parent:
            d += 1
            child = []
            for node in parent:
                if node.left is not None:
                    child.append(node.left)
                if node.right is not None:
                    child.append(node.right)
            parent = child
        return d
```

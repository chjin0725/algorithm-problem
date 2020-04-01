# 문제
![leetcode_1302](https://user-images.githubusercontent.com/51700219/78144597-c5ac9a00-746a-11ea-9a89-d5ccd86d03a3.png)
# 풀이
- lever order traversal 이용
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def deepestLeavesSum(self, root: TreeNode) -> int:
        if root is None:
            return 0
        
        parent = [root]
        
        while parent:
            child = []
            ans = 0
            for node in parent:
                ans += node.val
                if node.left is not None:
                    child.append(node.left)
                if node.right is not None:
                    child.append(node.right)
            parent = child
        return ans
```

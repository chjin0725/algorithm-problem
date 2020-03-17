# 문제
![leetcode_101](https://user-images.githubusercontent.com/51700219/76839629-2c319580-6879-11ea-8e42-fc8d4b75445f.png)

# 풀이
- bfs 혹은 dfs를 사용하면 되는데 큐 혹은 스택에 넣는 순서를 다르게 해주면 된다.
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
from collections import deque
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        if root is None:
            return True
        if root.left is None or root.right is None:
            if root.left is None and root.right is None:
                return True
            else:
                return False
        q1 = deque()
        q2 = deque()
        
        q1.append(root.left)
        q2.append(root.right)
        
        while q1 and q2:
            t1 = q1.popleft()
            t2 = q2.popleft()
            
            if t1.val != t2.val:
                return False
            
            if t1.left is not None or t2.right is not None:
                if t1.left is not None and t2.right is not None:
                    q1.append(t1.left)
                    q2.append(t2.right)
                else:
                    return False
            
            if t1.right is not None or t2.left is not None:
                if t1.right is not None and t2.left is not None:
                    q1.append(t1.right)
                    q2.append(t2.left)
                else:
                    return False
            
        return True
```
- 어렵진 않은 문제지만 False를 리턴해야 하는 경우가 어떤게 있는지 잘 생각해주어야 한다.

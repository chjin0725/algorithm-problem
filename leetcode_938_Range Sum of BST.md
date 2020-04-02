# 문제
![leetcode_938](https://user-images.githubusercontent.com/51700219/78265131-00800200-753f-11ea-9469-ecb3f3db0e02.png)
# 풀이
- 그냥 bst 문제임
- dfs로 순회하되 순회할 필요 없는 부분은 순회하지 않도록 하였다.
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def rangeSumBST(self, root: TreeNode, L: int, R: int) -> int:
        if root is None:
            return 0
        
        ans = 0
        
        s = [root]
        while s:
            cur = s.pop()
            if cur is not None:
                if L <= cur.val <= R:
                    ans += cur.val
                    s.append(cur.left)
                    s.append(cur.right)
                elif cur.val < L:
                    s.append(cur.right)
                else:
                    s.append(cur.left)
        return ans
```

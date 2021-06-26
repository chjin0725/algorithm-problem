
# 풀이
- dfs든 bfs든 쓰면 됨
- 다만 순회하면서 2진수 값을 10진수로 바꿔주도록 한다.
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sumRootToLeaf(self, root: TreeNode) -> int:
        s = [(root,root.val)]
        
        ans = 0
        while s:
            cur, value = s.pop()
            if cur.left is None and cur.right is None:
                ans += value
            else:
                if cur.left is not None:
                    s.append((cur.left,cur.left.val + 2*value))
                if cur.right is not None:
                    s.append((cur.right, cur.right.val + 2*value))
        
        return ans
```
- ``s.append((cur.left,cur.left.val + 2*value))`` 이 부분이 핵심이다. 이렇게 하면 리프 노드에서 10진수로 바꿔주는 작업을 할 필요없이
바로 써 줄수 있다. 2*value는 노드의 깊이가 아래로 깊어짐에 따라 2진수상에서 자리수가 한자리 올라가는 것이므로 2를 곱해주는 것이다.

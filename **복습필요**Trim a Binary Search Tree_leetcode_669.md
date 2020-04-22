# 문제
![leetcode_669](https://user-images.githubusercontent.com/51700219/79943670-6576aa00-84a4-11ea-80b5-8636540d5ca4.png)
# 풀이
- easy치고는 꽤 어려운 문제였다.
- 일단 root가 L과 R의 범위를 벗어나면 root를 바꿔야 하므로 그 작업을 먼저 한다.
- 그 다음에는 현재 노드에 대해서 왼쪽과 오른쪽 자식을 범위안에 오도록 계속 바꾼다.
- 두 자식이 둘다 범위안에 있다면 다음 노드로 넘어간다.
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def trimBST(self, root: TreeNode, L: int, R: int) -> TreeNode:
        root_root = TreeNode(0)
        
        while L > root.val or R < root.val:
            if L > root.val:
                root = root.right
            elif R < root.val:
                root = root.left
        
        s = [root]
        
        while s:
            cur = s[-1]
            if cur.left is not None and cur.left.val < L:
                cur.left = cur.left.right
            elif cur.right is not None and cur.right.val > R:
                cur.right = cur.right.left
            else:
                s.pop()
                if cur.left is not None:
                    s.append(cur.left)
                if cur.right is not None:
                    s.append(cur.right)
        
        return root
```

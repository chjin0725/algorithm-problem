
# 풀이
- level order이므로 bfs를 사용한다.
- 단 현재 노드가 어떤 레벨에 있는지를 계속 추적하기 위해 num_parent, num_child변수를 사용.
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

from collections import deque
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        ans = []
        if root is None:
            return ans
        
        q = deque()
        q.append(root)
        num_parent = 1
        num_child = 0
        level_val = []
        while q:
            cur = q.popleft()
            num_parent -= 1       
            level_val.append(cur.val)
            if cur.left is not None:
                q.append(cur.left)
                num_child += 1
            if cur.right is not None:
                q.append(cur.right)
                num_child += 1
                
            if num_parent == 0:
                num_parent = num_child
                num_child = 0
                ans.append(level_val)
                level_val = []
        
        return ans
```
- bfs이므로 시간복잡도는 o(n)이고 공간 복잡도는 완전이진트리의 리프노드개수이므로 o(n)이다.

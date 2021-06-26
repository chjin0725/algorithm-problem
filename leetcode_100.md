
# 풀이
- dfs 혹은 bfs로 돌면서 값을 비교해 나가면 될 것 같다.
- 값이 다른 경우 말고도 한쪽은 왼쪽 자식이 있는데 한쪽은 왼쪽 자식이 없다던가 하는 경우도 다뤄줘야 한다.
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        if p is None or q is None:
            if p == q:
                return True
            else:
                return False
        
        stack1 = [p]
        stack2 = [q]
        
        while stack1 and stack2:
            cur1 = stack1.pop()
            cur2 = stack2.pop()
            
            if cur1.val != cur2.val:
                return False
            
            if cur1.left is not None and cur2.left is not None:
                stack1.append(cur1.left)
                stack2.append(cur2.left)
            else: ## at least one of two left is None
                if cur1.left != cur2.left: ## if one left is None but another is not None
                    return False
            
            if cur1.right is not None and cur2.right is not None:
                stack1.append(cur1.right)
                stack2.append(cur2.right)
            else:
                if cur1.right != cur2.right:
                    return False
        
        return True
```

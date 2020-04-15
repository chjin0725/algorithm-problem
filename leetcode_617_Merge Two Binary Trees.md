# 문제
![leetcode_670](https://user-images.githubusercontent.com/51700219/79341265-7c7a4100-7f66-11ea-9940-88fe50b6bc26.png)
# 풀이
- level order로 순회하면서 왼쪽 차일드가 둘다 있으면 다음 순회에 방문할 수 있도록 하고 둘중 하나가 없으면 있는쪽을 차일드로 쓴다. 둘다 없으면 그냥 스킵.
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def mergeTrees(self, t1: TreeNode, t2: TreeNode) -> TreeNode:
        if t1 is None or t2 is None:
            return t1 if t1 is not None else t2
        
        # root = cur = TreeNode(0)
        s = [(t1, t2)]
        
        while s:
            child = []
            for nodes in s:
                cur1, cur2 = nodes
                cur1.val += cur2.val
                if cur1.left is not None or cur2.left is not None:
                    if cur1.left is None:
                        cur1.left = cur2.left
                    elif cur2.left is None:
                        pass
                    else:
                        child.append((cur1.left, cur2.left))
                        
                if cur1.right is not None or cur2.right is not None:
                    if cur1.right is None:
                        cur1.right = cur2.right
                    elif cur2.right is None:
                        pass
                    else:
                        child.append((cur1.right, cur2.right))
            s = child
        return t1
```

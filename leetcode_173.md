```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class BSTIterator:

    def __init__(self, root: TreeNode):
        self.root = root
        self.inorder = []
        
        self.push(root)

    def next(self) -> int:
        out = self.inorder.pop()
        self.push(out.right)
        return out.val

    def hasNext(self) -> bool:
        return (len(self.inorder) != 0)
        
    def push(self, node):
        cur = node
        while cur:
            self.inorder.append(cur)
            cur = cur.left
        
```

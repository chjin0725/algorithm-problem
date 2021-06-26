
# 풀이
- level order traversal 이용
- 다만 grand parent까지 고려해야 하기 때문에 이 부분을 어찌할지를 고민하였음.
- 그냥 현재 레벨의 노드를 방문할 때 현재 노드가 짝수이면 그 노드의 grand child의 값을 바로 확인 방법을 생각함.
- 그러나 이렇게 하면 방문한 노드를 다음레벨에 또 방문하게 되는 문제가 생김. 즉 grand child는 나중에 방문을 한번 더 하게됨. 게다가 이렇게 짜면 자식뿐만 아니라
자식의 자식이 None이 아닌지를 봐야하기 때문에 코드가 지저분해짐.
- 대신 현재 보고있는 노드의 부모가 짝수인지 아닌지를 표시해 줌.
- 이렇게 하면 현재 보고있는 노드의 부모가 짝수 일때 현재보고 있느 노드의 자식을 리스트에 append할 때 그 자식의 값을 그자리에서 더해주면 됨.
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sumEvenGrandparent(self, root: TreeNode) -> int:
        if root is None:
            return 0
        ans = 0
        parent = [(root, False)]
        while parent:
            child = []
            for node,have_even_parent in parent:
                if node.val % 2 == 0:
                    is_even = True
                else:
                    is_even = False
                    
                if node.left is not None:
                    if have_even_parent:
                        ans += node.left.val
                    child.append((node.left, is_even)) ## (child, True if parent is even else False)
                    
                if node.right is not None:
                    if have_even_parent:
                        ans += node.right.val
                    child.append((node.right, is_even))
            parent = child
        
        return ans
```

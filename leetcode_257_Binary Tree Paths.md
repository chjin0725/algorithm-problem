# 문제

# 풀이
- dfs로 순회하되 각 노드의 부모를 딕셔너리에 저장해서 나중에 path를 백트래킹 할 수 있게 하였다.
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def binaryTreePaths(self, root: TreeNode) -> List[str]:
        ans = []
        if root is None:
            return ans
        
        parent = dict()
        s = [root]
        
        while s:
            cur = s.pop()
            
            if cur.left is None and cur.right is None:
                path = str(cur.val)
                while cur in parent:
                    cur = parent[cur]
                    path = str(cur.val) + '->' + path
                ans.append(path)
                    
                
            else:
                if cur.left is not None:
                    s.append(cur.left)
                    parent[cur.left] = cur
                if cur.right is not None:
                    s.append(cur.right)
                    parent[cur.right] = cur
            
        return ans
```
- 여기서 백트래킹 하는 것 때문에 시간이 느려진다. 리프노드가 n개일 때 백트래킹하는 시간이 트리의 높이 h 만큼 이므로 시간은 nh이다.
- 공간 복잡도는 n


# 다른 풀이
- 매번 현재 노드까지의 path를 계산하여 스택에 넣어준다.
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def binaryTreePaths(self, root: TreeNode) -> List[str]:
        if not root:
            return []
        res, queue = [], collections.deque([(root, "")])
        while queue:
            node, ls = queue.popleft()
            if not node.left and not node.right:
                res.append(ls+str(node.val))
            if node.left:
                queue.append((node.left, ls+str(node.val)+"->"))
            if node.right:
                queue.append((node.right, ls+str(node.val)+"->"))
        return res

```
- 여기서는 스택에 튜플을 넣기 때문에 스택의 크기가 커지지만 첫번째 방법에서는 딕셔너리를 쓰기 때문에 전체적인 메모리 사용량은 그게 그거다.(실제로 둘다
공간복잡도는 100%의 파이썬 유저보다 적게 사용했다고 나왓음
- 그러나 여기서는 백트래킹을 안하기 때문에 시간복잡도는 n이다. 속도는 이건 83%나오고 위에거는 13% 나왔음.

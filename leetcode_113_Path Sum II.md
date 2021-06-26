
# 풀이
- dfs로 풀 되 백트래킹 할 수 있도록 딕셔너리를 사용하였다.
```python3
class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> List[List[int]]:
        ans = []
        if root is None:
            return ans
        parent = dict()
        s = [(root, root.val)]
        
        while s:
            cur, path_sum = s.pop()
            if cur.left is None and cur.right is None:
                if path_sum == sum:
                    temp = [cur.val]
                    while cur in parent:
                        cur = parent[cur]
                        temp.append(cur.val)
                    temp.reverse()
                    ans.append(temp)
            else:                
                if cur.left is not None:
                    parent[cur.left] = cur
                    s.append((cur.left, path_sum + cur.left.val))
                if cur.right is not None:
                    parent[cur.right] = cur
                    s.append((cur.right, path_sum + cur.right.val))
                
        return ans
```

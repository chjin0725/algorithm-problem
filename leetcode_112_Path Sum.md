# 문제
![leetcode_112](https://user-images.githubusercontent.com/51700219/77750401-0e2d1780-7067-11ea-96a3-811533bcc039.png)

# 풀이
- dfs 문제이다.
- 다만 노드 값이 음수도 될 수 있다는 생각을 못해서 처음에는 틀렸다.
- 문제의 조건에 대해서 생각해보는 습관이 중요하다. 멋대로 값이 양수만 있을거라 생각하면 안됨.
```python3
class Solution:
    def hasPathSum(self, root: TreeNode, sum: int) -> bool:
        if root is None:
            return False
        s = [(root, root.val)]
        while s:
            cur, path_sum = s.pop()
            if cur.left is None and cur.right is None:
                if path_sum == sum:
                    return True
            else:                
                if cur.left is not None:
                    s.append((cur.left, path_sum + cur.left.val))
                if cur.right is not None:
                    s.append((cur.right, path_sum + cur.right.val))
        return False
```

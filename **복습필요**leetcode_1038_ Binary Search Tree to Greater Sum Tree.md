# 문제
![leetcode_1038](https://user-images.githubusercontent.com/51700219/78223133-57ff7d00-7501-11ea-9377-63bbf91955cb.png)
# 풀이
- 오른쪽 노드 -> 루트 -> 왼쪽 노드 순으로 중위순회 한다.
- 재귀말고 반복으로 짜는 법을 알아두기
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def bstToGst(self, root: TreeNode) -> TreeNode:
        cur = root
        s = []
        ans = 0
        while True:
            
            if cur is not None:
                s.append(cur)
                cur = cur.right
            elif s:
                cur = s.pop()
                ans += cur.val
                cur.val = ans                
                cur = cur.left
            else:
                break
        return root
```


# 풀이
- 중위 순회하는 코드를 짜면 된다.
- 재귀로는 쉽지만 반복으로 짜는게 쉽지 않다.
- 아무래도 재귀를 반복으로 푸는 연습을 더 해야 할 것 같다. 반복으로 푸는 법이 잘 안떠오른다.
```python3
class Solution:
    def increasingBST(self, root: TreeNode) -> TreeNode:
        if root is None:
            return root
        s = []
        cur = root
        ans = TreeNode('root')
        temp = ans
        while True:
            if cur is not None:
                s.append(cur)
                cur = cur.left
            elif s:
                cur = s.pop()
                temp.right = cur
                temp = temp.right
                cur.left = None
                cur = cur.right
            else:
                break
        return ans.right
            
```

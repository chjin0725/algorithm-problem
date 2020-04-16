# 문제
![leetcode_590](https://user-images.githubusercontent.com/51700219/79458443-c6c5f580-802c-11ea-9274-28df929da3f4.png)
# 풀이
- postorder 이므로 스택에 자식노드를 넣을 때 오른쪽 부터 넣는다.
```python3
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""

class Solution:
    def postorder(self, root: 'Node') -> List[int]:
        ans = []
        if root is None:
            return []
        s = [[root, False]]
        
        while s:
            cur = s[-1]
            if cur[0].children and not cur[1]:
                for i in range(len(cur[0].children)-1, -1, -1):
                    s.append([cur[0].children[i], False])
                cur[1] = True ## 이런 flag 안쓰고 그냥 cur.children = None으로 해도 될 듯.
            else:
                cur = s.pop()[0]                
                ans.append(cur.val)
                
        return ans
```

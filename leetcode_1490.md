- tree문제이다.
- 그래프문제는 대부분 dfs,bfs를 사용한다.
- 만일 트리문제라면 여기서 추가로 preorder, inorder, postorder, level order를 생각해봐야한다.
- 이 문제는 dfs로 풀었다.

```python3
class Solution:
    def cloneTree(self, root: 'Node') -> 'Node':
        if not root:
            return None
        
        root_copy = self.dfs(root)
        
        return root_copy
    
    def dfs(self, p):
        copy = Node(p.val)
        
        if p.children:
            copy.children = []
            for child in p.children:
                copy.children.append(self.dfs(child))
        
        return copy
```

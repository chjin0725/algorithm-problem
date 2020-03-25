# 문제
![leetcode_993](https://user-images.githubusercontent.com/51700219/77531776-d55e3880-6ed6-11ea-9304-490db5a81a66.png)
# 풀이
- 이진트리를 순회하면 된다.
- bfs, dfs등을 쓸 수 있으나 그냥 이진트리를 depth별로 순회하도록 구현해 보았다.
- bfs도 depth별로 순회하는 것이긴 하나 현재 노드가 어떤 depth에 있는지를 계속 추적해줘야 한다.
- 이번에 내가 구현한 코드는 while문 한번 돌 때 마다 현재 depth의 모든 노드를 방문하도록 구현했기 때문에 depth를 알기가 쉽다. while문을 돌때마다
depth를 +1 해주면 된다.
```python3
class Solution:
    def isCousins(self, root: TreeNode, x: int, y: int) -> bool:
        if root is None or root.val == x or root.val == y:
            return False

        found = dict()
        
        nodes = [root]
        
        d = 0
        while nodes:
            child = []
            for node in nodes:
                if node.left is not None:
                    child.append(node.left)
                    if node.left.val == x or node.left.val == y:
                        found[node.left.val] = (d+1, node) ## depth, parent
                
                if node.right is not None:
                    child.append(node.right)
                    if node.right.val == x or node.right.val == y:
                        found[node.right.val] = (d+1, node)
            
            if len(found) == 2:
                x_d, x_parent = found[x]
                y_d, y_parent = found[y]
                if x_d == y_d and x_parent != y_parent:
                    return True
                else:
                    return False
            
            nodes = child
            d += 1
        return False
```
- 다만 여기서 nodes뿐만 아니라 child도 있기 때문에 메모리 사용량이 좀 많아진다. 

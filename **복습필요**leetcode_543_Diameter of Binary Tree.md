# 문제
![leetcode_543](https://user-images.githubusercontent.com/51700219/79039364-bae8c680-7c1b-11ea-96c8-760f5463b2de.png)
# 풀이
- 왼쪽 -> 오른쪽 -> 루트 순으로 순회하는 post order를 이용.
- 왼쪽과 오른쪽 서브트리의 높이를 계산해두고 루트를 방문 할때 왼쪽과 오른쪽의 서브트리의 최대값을 루트의 높이로 하면 된다.
- 이때 왼쪽 서브트리와 오른쪽 서브트리의 높이를 합한 값이 현재까지 계산한 diameter보다 큰지 확인한다.
- 근데 후위순회를 구현하려하니까 되게 헷갈린다.
- bfs든 dfs든 각각의 순회든 방문할 때 pop한다는 것을 기억하자. 방문하는게 아니면 그냥 s[-1]로 스택의 가장 높은 값을 조회만 한다.

```python3
class Solution:
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        if root is None:
            return 0
        
        s = [root]
        h = dict()
        ans = 0
        # cur = root
        while s:
            cur = s[-1]
            if cur.left is not None and cur.left not in h:
                s.append(cur.left)
            elif cur.right is not None and cur.right not in h:
                s.append(cur.right)
            
            else:
                cur = s.pop()
                left_h = 0 if cur.left not in h else h[cur.left]
                right_h = 0 if cur.right not in h else h[cur.right]
                h[cur] = max(left_h, right_h) + 1
                ans = max(ans, left_h + right_h)
        
        return ans
```
- 처음에는 dfs로는 안되는 줄 알았다. dfs는 top-down 방식이라고 생각했기 때문이다.
- 근데 생각해보니 dfs도 bottom-up 방식으로 할 수있다.
- 위의 코드처럼 s[-1]로 하고 leaf 노드 혹은 왼쪽 오른쪽 다 방문한 노드일때만 pop하면 bottom up 방식으로 할 수 있다.
- 다만 왼쪽자식과 오른쪽 자식이 이미 방문한 노드인지 확인하기 위해 딕셔너리나 셋을 써야 한다.

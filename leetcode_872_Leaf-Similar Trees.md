# 문제
![leetcode_872](https://user-images.githubusercontent.com/51700219/77659037-e4b6b200-6fba-11ea-8353-d689e0064a28.png)

# 풀이
- dfs를 이용하여 풀었다. 단 스택에 노드를 넣을때 오른쪽 자식먼저 넣고 그다음 왼쪽자식을 넣는다.
```python3
class Solution:
    def leafSimilar(self, root1: TreeNode, root2: TreeNode) -> bool:
        seq1 = self.leafSequence(root1)
        seq2 = self.leafSequence(root2)
        
        if len(seq1) != len(seq2):
            return False
        else:
            for i in range(len(seq1)):
                if seq1[i] != seq2[i]:
                    return False
            return True
        
    def leafSequence(self, root):
        ans = []
        if root is None:
            return ans
        
        s = [root]
        
        while s:
            cur = s.pop()
            if cur.left is None and cur.right is None:
                ans.append(cur.val)
            else:
                if cur.right is not None:
                    s.append(cur.right)
                if cur.left is not None:
                    s.append(cur.left)
                
        return ans
```

# 개념 정리
- dfs,bfs,pre order, in order, post order은 전부 다른 순회방법이라 생각했다.
- 근데 그렇지 않다. dfs, bfs는 search의 한 방법이다.
- inorder, postorder,preorder는 이진 트리를 순회하는 방식을 말한다.
- 사실 위의 세 방식은 전부 dfs방식이다. 그래서 실제로 구현할때도 스택을 사용한다.

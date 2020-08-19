## 문제
![20200818_010340](https://user-images.githubusercontent.com/51700219/90417451-aeefa280-e0ee-11ea-824a-7b873960915c.png)

## 풀이
 - 정렬된 배열에서 두 숫자의 차이의 절대값의 최소값을 찾는 것과 같다.
 - 인접한 두 숫자의 차이를 비교하면 된다.
 - 이를 BST에서 하려면 in order로 순회한다. 단, 이전 값을 추적해야 하므로 self.pre를 사용했다.
 ```python3
 class Solution:
    def minDiffInBST(self, root: TreeNode) -> int:
        self.ans = float('inf')
        self.pre = float('-inf')
        self.inorder(root)
        return self.ans
    
    def inorder(self, node):
        if node.left is not None:
            self.inorder(node.left)
            
        self.ans = min(self.ans, abs(node.val - self.pre))
        self.pre = node.val
        
        if node.right is not None:
            self.inorder(node.right)
 ```

## 반복으로 풀이
```python3
    def minDiffInBST(self, root: TreeNode) -> int:
        pre = float('-inf')
        ans = float('inf')
        s = []
        cur = root
        while True:
            if cur is not None:
                s.append(cur)
                cur = cur.left
                
            elif s:
                cur = s.pop()
                ans = min(ans, abs(pre - cur.val))
                pre = cur.val
                cur = cur.right
            
            else:
                break
        return ans
```
 - 스택에 append해주는건 cur 뿐이다.
 - 다만 cur을 cur.left 혹은 cur.right로 상황에 맞게 바꿔준다.
 - cur을 방문(cur에 대해서 ans,pre를 계산하는 작업)하기 전에는 cur을 cur.left로 계속 바꿔주고 방문하고나서 cur.right으로 바꿔주는 것임.

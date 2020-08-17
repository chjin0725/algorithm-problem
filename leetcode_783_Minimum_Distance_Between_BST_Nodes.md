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

# 문제

# 풀이
- 아마 재귀 혹은 반복으로 풀 수 있을 것 같았는데 반복으로 할 방법은 바로 생각나진 않았다.( 피곤하기도 했고...)
- 재귀를 이용하여 풀어주었다. 재귀를 이용하면 위에서 부터 밑으로 타고 가는데 이미 밑에서 unbalance가 일어난 경우 False를 리턴하도록 하였다.
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        if root is None or self.get_height(root, 1):
            return True
        else:
            return False
        
    
    def get_height(self, node, h):
 
        if node.left is not None:
            left_h = self.get_height(node.left, h+1)
            if left_h == False:
                return False
        else:
            left_h = h
        
        if node.right is not None:
            right_h = self.get_height(node.right, h+1)
            if right_h == False:
                return False
        else:
            right_h = h
        
        if abs(left_h-right_h) > 1:
            return False
        else:
            return max(left_h, right_h)
```
- 이번 문제부터는 답지를 안보려고 했는데 이 문제는 생각해내는데 꽤 오래 걸렸다.
- 그래도 답지 안보고 풀어내니 뿌듯하긴 하다. 공부한 느낌도 들고

```python3
class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        def get_height( node, h):

            if node.left is not None:
                left_h = get_height(node.left, h+1)
                if left_h == False:
                    return False
            else:
                left_h = h

            if node.right is not None:
                right_h = get_height(node.right, h+1)
                if right_h == False:
                    return False
            else:
                right_h = h

            if abs(left_h-right_h) > 1:
                return False
            else:
                return max(left_h, right_h)
        
        
        
        if root is None or get_height(root, 1):
            return True
        else:
            return False
```
- 이런식으로 함수안에 함수를 정의해서 할 수도 있다.
- 근데 왜인지는 모르겠지만 속도가 좀 느려지고 메모리 사용량도 좀 늘어났다.
# 다른 풀이
- 재귀는 stack overflow를 항상 주의해야 한다.
- 가능하면 iterative한 방법으로 푸는게 좋다. 다만 재귀가 코드이해가 더 쉽다고 한다(나는 딱히 모르겠음)
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        if root is None:
            return True
        
        s = [root]
        h = dict()
        while s:
            cur = s[-1]
            if cur.left is not None and cur.left not in h:
                s.append(cur.left)
            elif cur.right is not None and cur.right not in h:
                s.append(cur.right)
            else:
                cur = s.pop()
                left_h = 0 if cur.left is None else (h[cur.left]+1)
                right_h = 0 if cur.right is None else (h[cur.right]+1)
                
                if abs(left_h-right_h) > 1:
                    return False
                
                h[cur] = max(left_h, right_h)
        
        return True
```
- 전위, 중위, 후위 순회는 전부 스택하나로 구현할 수 있다.
- 조금 깔끔하게 짜보려고 노력했는데 꽤 깔끔하게 짠 것 같다.

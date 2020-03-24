# 문제
![leetcode_108](https://user-images.githubusercontent.com/51700219/77426427-cc5a6200-6e17-11ea-8b2b-713ad8489c28.png)
# 풀이
- 알고리즘 자체가 어렵진 않다. 중간에 있는 값을 root로 그 왼쪽에 있는 값들을 left sub tree로, 오른쪽도 같은 방식으로 해주면 된다.
- 중간에 값을 root로 했으면 왼쪽에서 root전까지에 대해서 재귀적으로 똑같이 해주면 될 것이다.
- 근데 재귀는 항상 스택오버플로우의 위험이 있으니까 반복으로 구현하려 했다.
- 근데 반복으로 구현하려 하니 어떻게 구현할지가 떠오르지 않았다.
- 그래서 재귀로는 어떻게 구현할 까 생각해 봤는데 재귀함수의 인수로 부모노드, sub tree에 들어갈 값들의 인덱스 범위를 주면 된다.
- 여기서부터 반복을 구현하는 방법은 생각하기 쉽다. 재귀함수의 인수를 반복에서는 스택(dfs일 경우) 혹은 큐(bfs일 경우)에 넣어주면 된다.
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> TreeNode:
        if not nums:
            return None
        lo = 0
        hi = len(nums) - 1
        mid = (hi+lo)//2
        root = TreeNode(nums[mid])
        
        s = [(root,lo,hi)]
        
        while s:
            cur, lo, hi = s.pop()
            
            if lo == hi: ## means cur is leaf node
                continue
            
            else:
                mid = (lo + hi)//2
                
                left_lo = lo
                left_hi = mid-1
                if left_lo <= left_hi:
                    cur.left = TreeNode(nums[(left_lo + left_hi)//2])
                    s.append((cur.left, left_lo, left_hi))
                
                right_lo = mid + 1
                right_hi = hi
                if right_lo <= right_hi:
                    cur.right = TreeNode(nums[(right_lo + right_hi)//2])
                    s.append((cur.right, right_lo, right_hi))
                    
        return root
```
- 반복 구현방법이 안떠오르면 일단 재귀로는 어떻게 구현하는지를 생각해보자. 그러면 반복에 대한 구현방법이 자연스럽게 떠오른다.

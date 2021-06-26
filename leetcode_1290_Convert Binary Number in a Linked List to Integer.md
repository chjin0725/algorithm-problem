
# 풀이
- 하나씩 읽으면서 비트를 shift해주면 된다.
```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getDecimalValue(self, head: ListNode) -> int:
        ans = head.val
        cur = head.next
        while cur is not None:
            ans <<= 1
            ans += cur.val
            cur = cur.next
            
        return ans
```

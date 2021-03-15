```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def nextLargerNodes(self, head: ListNode) -> List[int]:
        out = []
        i = 0
        s = [] # [val, index]
        while head is not None:
            while s and s[-1][0] < head.val:
                _ , index = s.pop()
                out[index] = head.val
            s.append([head.val, i])
            i += 1
            out.append(0)
            head = head.next
        return out
```

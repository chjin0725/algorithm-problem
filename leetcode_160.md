```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        cur_a = headA
        cur_b = headB
        
        len_a = 0
        len_b = 0
        
        while cur_a:
            len_a += 1
            cur_a = cur_a.next
        
        while cur_b:
            len_b += 1
            cur_b = cur_b.next
        
        cur_a = headA
        cur_b = headB
        
        while len_a > len_b:
            cur_a = cur_a.next
            len_a -= 1
        
        while len_b > len_a:
            cur_b = cur_b.next
            len_b -= 1
        
        while cur_a != cur_b:
            cur_a = cur_a.next
            cur_b = cur_b.next
            
        
        return cur_a
```

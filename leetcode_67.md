```python
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        res = []
        
        n = max(len(a), len(b))
        
        carry = 0
        for i in range(n):
            index_a = len(a) - i - 1
            index_b = len(b) - i - 1
            
            if index_a >= 0:
                temp_a = int(a[index_a])
            else:
                temp_a = 0
            
            if index_b >= 0:
                temp_b = int(b[index_b])
            else:
                temp_b = 0
                
            res.append(str((temp_a + temp_b + carry) % 2))
            carry = 1 if (temp_a + temp_b + carry) >= 2 else 0
        
        if carry == 1:
            res.append(str(carry))
        
        res = res[::-1]
        
        return ''.join(res)
```

- two pointer를 이용하면 공간 복잡도를 상수로 하여 풀 수 있다.
```python3
class Solution:
    def reverseVowels(self, s: str) -> str:
        s = list(s)
        vowels = {'a','A','e','E','i','I','o','O','u','U'}
        
        i = 0
        j = len(s)-1
        
        while i < j:
            while s[i] not in vowels and i < j:
                i+=1
            
            while s[j] not in vowels and j > i:
                j-=1
            
            if i == j:
                break
            
            temp = s[i]
            s[i] = s[j]
            s[j] = temp
            i+=1
            j-=1
        
        return ''.join(s)
```

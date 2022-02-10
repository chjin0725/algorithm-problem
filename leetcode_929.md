```python3
class Solution:
    def numUniqueEmails(self, emails: List[str]) -> int:
        uniques = set()
        
        for email in emails:
            s = []
            local, domain = email.split('@')
            i = 0
            while i < len(local):
                if local[i] == '.':
                    i += 1
                elif local[i] == '+':
                    break
                else:
                    s.append(local[i])
                    i += 1
            s.append('@')
            s.extend(domain)
            
            uniques.add(''.join(s))
        
        return len(uniques)
```

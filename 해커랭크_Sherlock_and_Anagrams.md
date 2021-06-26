```python3
def sherlockAndAnagrams(s):
    n = len(s)
    ans = 0
    for l in range(1,n):
        substrings = defaultdict(int)
        for i in range(n-l+1):
            key = ''.join(sorted(s[i:i+l]))
            substrings[key] += 1
        for v in substrings.values():
            if v > 1:
                ans += int(v*(v-1)/2)
                
    return ans
```

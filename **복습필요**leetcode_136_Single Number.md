# 문제

# 풀이
- 해쉬나 셋을 쓰고 o(n)으로 풀 수는 있지만 공간복잡도를 o(1)으로 유지하면서 푸는 방법은 도저히 안떠올랐다.
- 알고보니 xor을 사용하면 된다.
- xor의 성질을 이용한다
- **A xor A = 0**
- **A xor B xor A = A xor A xor B = B**
```python3
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        xor = 0
        for num in nums:
            xor = xor^num
        return xor
```

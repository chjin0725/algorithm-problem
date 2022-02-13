- monotonic stack사용
- 내림차순으로 stack을 만든다.

```python3
class StockSpanner:

    def __init__(self):
        self.mono_stack = []
        self.index = 0

    def next(self, price: int) -> int:

        while self.mono_stack and self.mono_stack[-1][0] <= price:
            self.mono_stack.pop()
        self.mono_stack.append((price, self.index))
        self.index += 1
        
        if len(self.mono_stack) == 1:
            return self.index
        
        else:
            return (self.mono_stack[-1][1] - self.mono_stack[-2][1])

```

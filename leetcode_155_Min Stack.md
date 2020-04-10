# 문제
![leetcode_155](https://user-images.githubusercontent.com/51700219/78980648-4b120780-7b59-11ea-9520-12d5c525f7ae.png)
# 풀이
- 스택에 push할 때 지금까지의 최소값을 튜플로 같이 푸쉬해준다.
```python3
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.s = []
        

    def push(self, x: int) -> None:
        temp = self.getMin()
        if temp is None:
            self.s.append((x,x))
        else:
            self.s.append((x, min(x, temp)))

    def pop(self) -> None:
        if self.s:
            return self.s.pop()[0]

    def top(self) -> int:
        if self.s:
            return self.s[-1][0]

    def getMin(self) -> int:
        if self.s:
            return self.s[-1][1]
        else:
            return None
        


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```

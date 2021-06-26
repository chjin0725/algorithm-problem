
# 풀이
- 예제를 몇개 손으로 풀어보면 happy number가 아닌 것은 cycle이 존재함을 알 수 있다.
- 즉 이전에 나왔던 숫자가 또 나와서 절대 1이 될 수가 없음.
- cycle이 없는 숫자는 언젠가는 1이 된다.
- 각 digit의 제곱을 더하는 것이기 때문에 처음 숫자가 아무리 커도 금방 두자리 숫자가 되버림.
```python3
class Solution:
    def isHappy(self, n: int) -> bool:
        seen = set()
        while True:
            if n == 1:
                return True
            elif n in seen:
                return False
            else:
                seen.add(n)
                n = self.digitSum(n)
    def digitSum(self, n):
        res = 0
        while n != 0:
            res += (n%10)**2
            n = n//10
        return res
```

# 다른 풀이
- 링크드 리스트에서 사이클을 발견하는 알고리즘을 응용한다.
```python3
class Solution:
    def isHappy(self, n: int) -> bool:
        x = n
        y = n
        while True:
            x = self.digitSum(x)
            if x == 1:
                return True
            
            y = self.digitSum(y)
            y = self.digitSum(y)
            if y == 1:
                return True
                        
            if x==y:
                return False
            
    def digitSum(self, n):
        res = 0
        while n != 0:
            res += (n%10)**2
            n = n//10
        return res
```
- 포인터를 두개 사용하고 하나는 1칸씩 다른 하나는 2칸씩 이동하면 사이클이 있다면 언젠가는 두 포인터가 만나게 된다.
- 즉 2칸씩 이동하는 포인터는 1칸씩 이동하는 포인터를 건너뛰고 이동할 수 없다
- 왜 이게 항상 참일까?
- 첫번째 포인터를 p1, 두번째 포인터를 p2라 하자.
- p2가 p1을 건너띄었다고 가정해보자. [] -> [p1] -> [p2] 이런 상황일 것이다.
- 이런 상황의 바로 전 단계는 어떻게 될까?
- [p1,p2] -> [] -> [] 이렇게 될 것이다.
- 즉 [] -> [p1] -> [p2] 상황이 되기 전에 만나게 되는 것이다.
- proof by contradiction이다.

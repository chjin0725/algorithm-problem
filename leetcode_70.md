# 문제
![leetcode_70](https://user-images.githubusercontent.com/51700219/76623886-a0b5bd00-6577-11ea-9269-e6249eb59c8f.png)

# 풀이
- dp문제인것 같은 느낌이 처음부터 들었다.
- dp는 i-1번째 solution이 있을 때 i번째 solution을 어떻게 얻을지에 대한 고민으로 시작하면 된다.
- 여기서는 i-2번째 solution도 필요해 보인다.
- i-1번째 solution에서 한칸을 올라가거나 i-2번째 solution에서 2칸을 올라가면 된다.
- 즉, `sol[i] = sol[i-1] + sol[i-2]`이다. 피보나치 형태임.
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 1:
            return 1
        if n == 2:
            return 2
        pre = 2 ## (i-1)th solution
        pre2 = 1 ## (i-2)th solution
        
        for _ in range(n-2):
            temp = pre
            pre += pre2
            pre2 = temp
        
        return pre
```
- (i-1)번째와 (i-2)번째 solution만 있으면 되므로 굳이 리스트를 쓸 필요없다.

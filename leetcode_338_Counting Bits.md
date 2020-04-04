# 문제
![leetcode_338](https://user-images.githubusercontent.com/51700219/78432334-5aeca000-76b0-11ea-9050-cd80b6a420f9.png)

# 풀이
- dp인것을 미리 알고 문제를 본게 아니라면 dp인 것을 눈치채기가 힘든 문제인 것 같다.
- 그치만 그냥 모든 정수를 비트연산을 통해 1의 개수를 새는 식의 나이브한 풀이는 아닐거라고 생각할 순 있을 듯.
- 테스트 케이스 몇개를 풀어보면 풀이법을 떠올릴 수 있다.
- (현재 숫자 - 현재 숫자와 가장 가까운 2의 제곱)의 1의 개수에 +1을 해주면 된다.
- 즉 현재 숫자와 가장 가까운 2의 제곱의 1의 개수와 (현재 숫자 - 현재 숫자와 가장 가까운 2의 제곱)의 1의 개수를 더해주는 것이다.
```python3
class Solution:
    def countBits(self, num: int) -> List[int]:
        # if n == 0:
        #     return [0]
        # elif n == 1:
        #     return [0, 1]
        ans = [0]*(num+1)
        cur_power_of_two = 0
        next_power_of_two = 1
        
        for n in range(1,num+1):
            if n == next_power_of_two:
                cur_power_of_two = next_power_of_two
                next_power_of_two *= 2
                ans[n] = 1
            else:
                ans[n] = 1+ans[n-cur_power_of_two]
        
        return ans
```

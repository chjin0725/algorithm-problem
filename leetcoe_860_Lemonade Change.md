

# 풀이
- 잔돈 문제는 거의다 그리디 인듯.
- 로직이 그렇게 어렵진 않다. 10달러 까지는 별거 없고 20달러일 때는 10달러 있으면 먼저 반환하는 식으로 한다.
```python3
class Solution:
    def lemonadeChange(self, bills: List[int]) -> bool:
        change = dict()
        change[5] = 0
        change[10] = 0
        
        for pay in bills:
            if pay == 5:
                change[5] += 1
            else:
                if pay == 10:
                    change[10] += 1
                rest = pay - 5
                while rest != 0:
                    if rest >5 and change[10] != 0:
                        rest -= 10
                        change[10] -= 1
                    elif change[5] != 0:
                        rest -= 5
                        change[5] -= 1
                    else:
                        return False
        return True
```
# 다른 풀이
```python3
class Solution:
    def lemonadeChange(self, bills: List[int]) -> bool:
        change5 = 0
        change10 = 0
        
        for pay in bills:
            if pay == 5:
                change5 += 1
            elif pay == 10:
                change10 += 1
                change5 -= 1
            elif change10 > 0:
                change10 -= 1
                change5 -= 1
            else:
                change5 -= 3
            if change5 < 0:
                return False
        return True
```
- bunch of if statement라 가독성은 별로임.
- 다만 맨마지막에 change5가 음수이면 무조건 False를 리턴하고 있음. 이문제를 잘 이해해야 저렇게 코딩할 수 있는 것같다.
- 어떤 경우에든 change5가 음수면 잔돈이 부족한 상황이라는 것.

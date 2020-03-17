# 문제
![leetcode_441](https://user-images.githubusercontent.com/51700219/76841121-af53eb00-687b-11ea-975b-e2e4e23aa0ca.png)

# 풀이
- 그냥 중학교 수학문제 같은 문제이다.
- k*(k+1)/2 = n 을 만족하는 양수의 k값을 찾아서 소수점을 없애주면 된다. 소수점 없애는것은 실수에 int를 씌우면 된다.(floor(k)는 소수점을 없애는게 아니라 
k보다 작으면서 가장 큰 정수를 반환한다.)
```python3
class Solution:
    def arrangeCoins(self, n: int) -> int:
        return int(((-1+(1+8*n)**0.5)/2))
```
- 이런 문제는 딱히 인터뷰에 나오거나 할 것 같진 않다.
- 그래서 thumb up이 269인데 thumb down은 571이나 되는 듯.
- 앞으로 thumb up이 thumb down보다 작은건 걍 풀지 말아야지.

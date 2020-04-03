# 문제
![leetcode_52](https://user-images.githubusercontent.com/51700219/76594240-e785c180-653b-11ea-88e1-ad5c0dda27f6.png)

# 풀이
- 처음에는 n^2의 방법을 생각해 냈다.
- `A[i][j] = max(i~j까지의 합, A[i][j-1], A[i+1][j])`
- A[i][j] 는 i~j까지 고려했을 때 maximum subarray의 sum 이다.
![leetcode_52_2](https://user-images.githubusercontent.com/51700219/76594481-a2ae5a80-653c-11ea-9a03-9b2bdd178605.jpg)
- 위의 그림처럼 하나의 테스트 케이스( 입력이 [-2, 1, -3, 4] 일 때)를 잡고 이걸 풀기위해 필요한 sub problem들을 트리형식으로 그렸더니 솔루션을 떠올리기가 쉬웠다.
- 이렇게 그리면 현재 문제가 sub problem들로 어떻게 풀리는지를 볼 수 있고 겹치는 sub problem의 존재 유무도 볼 수 있다.
- 이 방법은 자주 사용할 수 있을 것 같다.
- 그런데 알고보니 o(n)의 풀이법도 있었다.

# 다른 풀이
- 핵심은 **i-1번째 까지의 solution을 구했을 때 이를 i번째로 어떻게 확장시키느냐** 이다.
- 이건 모든 dp에 통용되는 접근법 인 것 같다. 절대 잊지 말자.
- i-1번째까지의 maximum subarray의 합을 구했다면 i번째에서의 maximum subarray의 합은 어떤게 될 수 있을까? 한번 깊게 고민해보면,
- `i번째까지의 maximum subarray의 합 = max(i-1번째까지의 maximum subarray의 합, i번째를 포함한 subarray의 합의 최대)` 임을 알 수 있다.
- i번째를 포함한 subarray의 합의 최대는 어떻게 알 수 있을까? 이것도 깊게 고민해보면,
- `i번째를 포함한 subarray의 합 = max(i-1번째를 포함한 subarray의 합 + nums[i], nums[i])` 임을 알 수 있다.
- 여기서는 되게 간단히 적었지만 실제로는 여러 테스트 케이스를 손으로 풀어가며 생각해봐야 생각날 수 있는 것이다.
```python3
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        length = len(nums)
        mat = [0] * length
        
        ## base case init
        mat[0] = ans = nums[0]
            
        for i in range(1,length):
            mat[i] = max(mat[i-1] + nums[i], nums[i])
            ans = max(ans, mat[i])
        
        return ans
  ```
  
  - 처음부터 o(n)은 생각도 안해보고 바로 o(n^2)의 풀이를 생각해서 o(n)은 생각해볼 기회도 없었던 것 같다.
  - dp문제를 만나면일단 o(n)부터 고민해보는게 좋을 것 같다. 안될거 같으면 그다음에 n^2을 고민해보는 식으로.

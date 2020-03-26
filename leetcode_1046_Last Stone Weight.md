# 문제
![leetcode_1046](https://user-images.githubusercontent.com/51700219/77644859-1755b000-6fa5-11ea-8eeb-51a255177eb4.png)

# 풀이
- 매번 가장 무게가 가장 큰 돌과 그다음 돌을 뽑기위해 sort를 해주는 식으로 풀었다.
```python3
class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        while len(stones) > 1:
            stones.sort()
            first = stones.pop()
            sec = stones.pop()
            result = first - sec
            if result > 0:
                stones.append(result)
        
        if len(stones) == 0:
            return 0
        else:
            return stones[0]
```

# 다른 풀이
- 매번 가장 무게가 큰 돌을 뽑는다.
- 이건 완전히 max heap에 대한 문제이다. 즉 priority queue문제이다.
- 다만 priority queue문제를 많이 안 접해봐서 바로 생각이 안났다.
- 역시 이론만 공부하면 응용을 잘 못한다. 응용을 많이 해봐야 한다. 이건 어떤 분야든 마찬가지 인 듯.
```python3
import heapq
class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        stones = [-1*i for i in stones]
        heapq.heapify(stones)
        while len(stones) > 1:
            first = heapq.heappop(stones)
            second = heapq.heappop(stones)
            result = first - second
            if result < 0:
                heapq.heappush(stones, result)
        
        if len(stones) == 0:
            return 0
        else:
            return -stones[0]
```
- heapq를 사용하는 법을 알아두자.
- heapq는 리스트형태로 min heap을 구현한다. 위에서 heap.heapify(stones)를 해도 stones는 여전히 리스트이다. 다만 min heap에 맞게 원소들이 재배치 된다.
- min heap이므로 max heap처럼 쓰려면 원소에 -를 곱해주고 하는 트릭이 필요하고 다른 부분도 원소값이 -가 곱해진 것을 고려하여 구현해야한다.
- **최대값 혹은 최소값을 계속 뽑아서 쓰는 문제에서는 heap을 기억하자**

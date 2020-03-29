# 문제

# 풀이
- cost[0] 와 cost[1]의 차이가 큰 사람부터 어느 도시로 갈지를 배정한다. 가려는 도시의 자리가 남아있다면 cost가 적은 도시로 간다.
- cost[0] 와 cost[1]의 차이가 큰 사람부터 하는 이유는 만일 이런 사람을 나중에 했는데 자리가 없어서 cost가 비싼 곳으로 가야 할 경우 전체 cost의 합은
높아질 수 밖에 없기 때문이다.
```python3
class Solution:
    def twoCitySchedCost(self, costs: List[List[int]]) -> int:
        
        
        ans = 0
        for cost in costs:
            cost.append(abs(cost[0] - cost[1]))
            
        costs.sort(key = lambda x:x[2], reverse = True)
        num_A = num_B = 0
        limit = len(costs)/2
        

        for cost in costs:
            if cost[0] <= cost[1]:
                if num_A < limit:
                    ans += cost[0]
                    num_A += 1
                else:
                    ans += cost[1]
                    num_B += 1
                    
            else:
                if num_B < limit:
                    ans += cost[1]
                    num_B += 1
                else:
                    ans += cost[0]
                    num_A += 1
        
        return ans
```

-  더 로직이 간단하다.
```python3
def twoCitySchedCost(self, costs: List[List[int]]) -> int:
        costs.sort(key=lambda cost: cost[0] - cost[1])
        costs_for_A = sum([cost[0] for cost in costs[:len(costs) // 2]])
        costs_for_B = sum([cost[1] for cost in costs[len(costs) // 2:]])
        return costs_for_A + costs_for_B
```

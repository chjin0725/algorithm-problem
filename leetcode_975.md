- 문제 링크: https://leetcode.com/problems/odd-even-jump/
- hard문제이다. 어렵긴 한데 노력으로 뚫어볼 수 있을 만한 것 같다.
- 먼저 odd jump, even jump의 의미를 잘 생각해봐야 한다.
- odd jump만 먼저 생각해보면 배열에서 현재 위치의 오른쪽에 있는 값들 중에 현재위치 값 이상이면서 가장 작은 값의 위치로 점프하는 것이다.
- 이를 다시 생각해보자. 현재위치 값 이상이면서 가장 작은 값이라 함은??
- 오름차순으로 정렬했을 때 바로 오른쪽에 있는 값이다.
- 예컨데 배열이 [5,1,3,4,2] 라면 1에서 odd jump를 하면 2이로 이동하게 되고 배열을 정렬했을 때 2는 1의 바로 오른쪽에 위치하는 값이기도 하다.
- 다만 odd jump를 하려면 2의 위치가 1보다 오른쪽에 있어야 한다. 즉, 2의 인덱스가 1의 인덱스보다 커야한다.
- 이때 단조스택을 사용할 수 있다. 이 경우 배열의 값이 아닌 인덱스 기준으로 단조스택을 사용한다.
- 정렬된 배열에서 현재 스택의 top에 있는 인덱스가 새로들어올 인덱스보다 작다면 pop한다. 이때 pop된 인덱스에 대한 odd jump(혹은 even jump)후의 위치는 새로들어올 인덱스가 된다.
- 정말 어렵긴 하지만 배운 것들을 잘 응용하면 풀 수 있다.

```python3
class Solution:
    def oddEvenJumps(self, arr: List[int]) -> int:
        n = len(arr)
        
        next_higher = [0]*n ## index of next higher
        arr_sorted = [(e,i) for i,e in enumerate(arr)]
        arr_sorted.sort(key = lambda x : (x[0], x[1]))
        
        s = []
        for _, i in arr_sorted:
            while s and s[-1] < i:
                next_higher[s.pop()] = i
            s.append(i)
            
        next_lower = [0]*n ## index of next lower
        arr_sorted = [(e,i) for i,e in enumerate(arr)]
        arr_sorted.sort(key = lambda x : (-x[0], x[1]))
        
        s = []
        for _, i in arr_sorted:
            while s and s[-1] < i:
                next_lower[s.pop()] = i
            s.append(i)
        
        odd = [0]*n
        even = [0]*n
        odd[-1] = even[-1] = 1
        
        for i in range(n-2, -1, -1):
            odd[i] = even[next_higher[i]]
            even[i] = odd[next_lower[i]]
        
        return sum(odd)
```

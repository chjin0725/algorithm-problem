```python
from collections import defaultdict
class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        '''Check if it is possible to pick up every passengers.
        
        Args:
            trips (list): trips[i] = [num_passengers, start_location, end_location]
            capacity (int): # of empty seats
        
        Returns:
            Boolean : True if possible to pick up every passengers
        '''
        
        num_passengers = defaultdict(int)
        for n,s,e in trips:
            num_passengers[s] += n
            num_passengers[e] -= n
            
        num_passengers_sort = sorted(num_passengers.items())
        
        # print(num_passengers_sort)
        
        num_seats = capacity
        for e in num_passengers_sort:
            num_seats -= e[1]
            if num_seats < 0:
                return False
        
        return True
```

- bfs로 푸는 문제이다.
- 따라서 adjecency list가 필요하다.
- 처음 풀이는 다음과 같다.

```python3
from collections import defaultdict, deque

class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        visited = set()
        q = deque()
        
        adj = defaultdict(list)
        for i in range(len(wordList)):
            if self.is_neighbor(beginWord, wordList[i]):
                q.append([wordList[i],2])
                visited.add(wordList[i])
            for j in range(i+1, len(wordList)):
                if self.is_neighbor(wordList[i], wordList[j]):
                    adj[wordList[i]].append(wordList[j])
                    adj[wordList[j]].append(wordList[i])
        
        visited.add(beginWord)
        while q:
            cur, num_word = q.popleft()
            
            if cur == endWord:
                return num_word
            
            
            for nei in adj[cur]:
                if nei not in visited:
                    q.append((nei, num_word+1))
                    visited.add(nei)
        return 0
        
    def is_neighbor(self, w1, w2):
        num_diff = 0
        
        for i in range(len(w1)):
            if w1[i] != w2[i]:
                num_diff += 1
        
        return True if num_diff == 1 else False
```
- 이렇게 하니 시간초과가 발생했다.
- 문제는 adjecency list를 만들 때 for문을 두번 돌면서 노드개수 제곱만큼의 연산량이 필요하기 때문이다.
- 최대 노드개수가 5000이므로 최대 25000000만큼의 연산량이 추가될 수 있다. 천만단위까지 가면 보통 시간초과가 뜬다.
- 그럼 이 부분을 개선하면 될까 싶었는데 또 생각해보니 while문에서 걸리는 시간은 edge 개수만큼 걸릴 수 있고 보통 그래프에서 edge 개수는 최대 노드개수 제곱만큼 커질 수 있다. 그래서 adjecency list를
만드는 시간을 줄여도 어차피 while문 안에서 노드개수 제곱만큼의 시간이 걸릴 것이므로 소용 없을 것이라 생각하였다.
- 근데 input의 조건을 잘 생각해보면 그렇지 않다. 한 단어의 길이는 최대 10이라고 제한이 걸려있기 때문에 길이가 10인 한 단어와 연결 될 수 있는 다른 단어의 최대 개수는 269개 이다(10 * 27(알파벳개수) - 1).
- 그러므로 adjency list 생성하는 부분을 개선해주면 시간복잡도를 개선할 수 있다.
- 어차피 존재할 수 있는 인접노드의 종류는 제한이 있으므로 그걸 전부 확인해주는 식으로 만들어 준다.
```python3
from collections import defaultdict, deque

class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        wordList = set(wordList)
        q = deque()
        q.append([beginWord, 1])
        
        while q:
            cur, num_word = q.popleft()
            
            if cur == endWord:
                return num_word
            
            
            for c in 'abcdefghijklmnopqrstuvwxyz':
                for i in range(len(beginWord)):
                    neighbor_candidate = cur[:i] + c + cur[i+1:]
                    if neighbor_candidate in wordList:
                        q.append([neighbor_candidate, num_word+1])
                        wordList.remove(neighbor_candidate)
        return 0
```


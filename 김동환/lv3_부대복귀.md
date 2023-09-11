# Code 
----
1. 목적지 공통
2. 그럼 destination에서 bfs -> source 만나면 저장
3. source에서 bfs하면 시간복잡도 비효율(반복해야하기 때문)

```
from collections import defaultdict, deque
import math
    
def solution(n, roads, sources, destination):
    answer = []
    
    graph = defaultdict(set)

    for path in roads:
        s, d = path
        graph[s].add(d)
        graph[d].add(s)
           
    result = bfs(destination, set(sources), graph)
    return [result[s] for s in sources]

def bfs(destination, sources, graph):
    q = deque()
    q.append((destination, 0))
    visited = set()
    result = {}
    
    for s in sources: result[s] = -1
        
    while q:
        curr, d = q.popleft()
        if curr not in visited:
            visited.add(curr)
            
            if curr in sources:
                result[curr] = d
            
            neighbors = graph[curr]
            for n in neighbors:
                q.append((n, d + 1))     
    return result
        
    
    
    

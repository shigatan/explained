# Graph Checklist

- BFS

```python
def bfs(s:int, G:dict):
    # s - source vertex
    # G - adjacencies map
    q = [s]
    level = {s:0}
    parent = {s:None}
    i = 1
    while q:
        next = []
        for v in q:
            for v1 in G[v]:
                if v1 not in level:
                    parent[v1] = v
                    level[v1] = i
                    next.append(v1)
        q = next
        i += 1
    return
```

- DFS recursive

```python
parent = {}
def dfs(V:List[int], G:dict):
    # V - set of vertexes
    # G - adjacencies map
    for s in V:
        if s not in parent:
            parent[s] = None
            dfsVisit(v, G)
    return

def dfsVisit(v:int, G:dict):
    for v1 in G[v]:
        if v1 not in parent:
            parent[v1] = v
            dfs-visit(v1, G)
    return
```

- DFS iterative

```python
def dfs(s:int, G:dict):
    # s - source vertex
    # G - adjacencies map
    stack = [s]
    parent = {s:None}
    while stack:
        v = stack.pop()
        for v1 in G[v]:
            if v1 not in parent:
                parent[v1] = v
                stack.append(v1)
    return
```

- Topological sort

```python
parent = {}
order = []
def topologicalSort(V:List[int], G:dict) -> List[int]:
    # V - set of vertexes
    # G - adjacencies map
    for s in V:
        if s not in parent:
            parent[s] = None
            dfsVisit(s, G)

    return reversed(order)

def dfsVisit(v:int, G:dict):
    for v1 in G[v]:
        if v1 not in parent:
            parent[v1] = v
            dfsVisit(v1, G)

    order.append(v)
    return
```

- Cycle detection

```python
visited = set()
recStack = set()
def hasCycle(V:List[int], G:dict)-> bool:
    # V - set of vertexes
    # G - adjacencies map
    for s in V:
        if s not in visited:
            visited.add(v)
            if hasCycleUtil(s, G):
                return True

    return False

def hasCycleUtil(v:int, G:dict) -> bool:
    recStack.add(v)
    for v1 in G[v]:
        if v1 not in parent:
            visited.add(v)
            if hasCycleUtil(v1, G):
                return True
        elif v1 in recStack:
            return True

    recStack.remove(v)
    return False
```

- Dijkstra

```python
def Dijkstra(s:int, t:int, G:dict) -> int:
    # s - source vertex
    # t - target vertex
    # G - adjacencies map
    parent = {s:None}
    dist = {s:0}
    q = [(0, s)]
    visited = set()
    while q:
        v = heapq.heappop(q)[1]
        if v in visited: continue
        visited.add(v)
        for neigh, weight in G[v]:
            d = dist[v] + weight
            # relaxation of edge
            if neigh not in dist or d < dist[neigh]:
                p[neigh] = v
                dist[neigh] = d
                heapq.heappush(q, (d, neigh))

    order = [t]
    p = parent[t]
    while p:
        order.append(p)
        p = parent[p]

    print(f"shortest path from {s} to {t}: {d[t]}")
    print(f"shortest path from {s} to {t}: {" -> ".join(reversed(order))}")
    return
```

- Bellman-Ford
- Bidirectional (bfs, Dijkstra)
- Longest path

## Topological Sort (DFS)

Similar to typical DFS. Mark the node visited in the beginning of the recursive function, and put the node in the stack at the end of the recursive function function. 

```python3
def topoSort(self, n: int, edges: List[List[int]]) -> List[int]:
    adj = [list() for _ in range(n)]
    for u, v in edges:
        adj[u].append(v)

    visited = [0] * n
    stack = list()

    def dfs(u):
        visited[u] = 1
        for v in adj[u]:
            if not visited[v]:
                dfs(v)
        stack.append(u)

    for u in range(n):
        if not visited[u]:
            dfs(u)

    return stack
```

If you also want to find cycles, add recursion stack `rec` to the above algorithm. Recursion stack helps you keep track of "back edge" - a node that points to one of its ancestors in a DFS tree.

```python3
def topoSort(self, n: int, edges: List[List[int]]) -> List[int]:
    adj = [list() for _ in range(n)] 
    for u, v in edges:
        adj[u].append(v)

    rec = [0] * n
    visited = [0] * n
    stack = list()

    def dfs(u):
        visited[u] = 1
        rec[u] = 1
        for v in adj[u]:
            if not visited[v]:
                if not dfs(v):
                    return False
            elif rec[v]:
                return False
        stack.append(u)
        rec[u] = 0
        return True

    for u in range(numCourses):
        if not visited[u] and not dfs(u):
            return list() # returning an empty list because a cycle was found

    return stack
```

## Topological Sort (BFS)

aka. Kahn's algorithm. Keep checking for neighbors where indegree is zero. Useful for cycle detection.

```python3
def topoSort(self, n: int, edges: List[List[int]]) -> List[int]:
    adj = [list() for _ in range(n)]
    indegree = [0 for _ in range(n)]
    for u, v in edges:
        adj[v].append(u)
        indegree[u] += 1

    q = deque()
    res = list()

    for v in range(n):
        if indegree[v] == 0:
            q.append(v)

    while q:
        v = q.popleft()
        res.append(v)
        for nei in adj[v]:
            indegree[nei] -= 1
            if indegree[nei] == 0:
                q.append(nei)

    # cannot find topo order due to cycles
    if len(res) != n: 
        return []
    return res
```

## Union Find

```python3
class UnionFind:
    def __init__(self, size):
        self.parent = [i for i in range(size)]
        self.rank = [1] * size

    def find(self, u):
        if self.parent[u] == u:
            return u
        self.parent[u] = self.find(self.parent[u])
        return self.parent[u]

    def union(self, u, v):
        u = self.find(u)
        v = self.find(v)
        if u == v:
            return
        if self.rank[u] < self.rank[v]:
            self.parent[u] = v
            self.rank[v] += self.rank[u]
        else:
            self.parent[v] = u
            self.rank[u] += self.rank[v]
```
      

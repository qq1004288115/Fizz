
## Leetcode

#### DFS
```
class Solution:
    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:
        graph = collections.defaultdict(set)
        def dfs(start, end):
            if start not in visited:
                visited.add(start)
                if start == end:
                    return True
                return any(dfs(nxt, end) for nxt in graph[start])
        for u, v in edges:
            visited = set()
            if u in graph and v in graph and dfs(u, v):
                return u, v
            graph[u].add(v)
            graph[v].add(u)
```

```
class Solution:
    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:
        parent = list(range(len(edges) + 1))
        for u, v in edges:
            uroot = self.find(u, parent)
            vroot = self.find(v, parent)
            if uroot == vroot:
                return u, v
            parent[uroot] = vroot
        
    def find(self, x, parent):
        if x != parent[x]:
            parent[x] = self.find(parent[x], parent)
        return parent[x]
```

## Union-Find
```
class dsu:
    def __init__(self):
        self.par = list(range(1001))
        self.rnk = [0] * 1001
    def find(self, x):
        while self.par[x] != x:
            x = self.par[x]
        return x
    def union(self, x, y):
        xroot, yroot = self.find(x), self.find(y)
        if xroot == yroot:
            return False
        elif self.rnk[xroot] < self.rnk[yroot]:
            self.par[xroot] = yroot
        elif self.rnk[xroot] > self.rnk[yroot]:
            self.par[yroot] = xroot
        else:
            self.par[yroot] = xroot
            self.rnk[xroot] += 1
        return True

class Solution:
    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:
        tmp = dsu()
        for edge in edges:
            if not tmp.union(*edge):
                return edge
```

```
class dsu:
    def __init__(self):
        self.par = list(range(1001))
    def find(self, x):
        if self.par[x] != x:
            self.par[x] = self.find(self.par[x])
        return self.par[x]
    def union(self, x, y):
        rootx, rooty = self.find(x), self.find(y)
        if rootx == rooty: return False
        self.par[self.find(x)] = self.find(y)
        return True
    
class Solution:
    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:
        tmp = dsu()
        for edge in edges:
            if not tmp.union(*edge):
                return edge
```

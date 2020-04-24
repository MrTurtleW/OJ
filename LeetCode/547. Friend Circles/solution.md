# DFS

```java
class Solution {
    private int[][] M;
    boolean[] visited;

    public int findCircleNum(int[][] M) {
        this.M = M;
        visited = new boolean[M.length];
        int count = 0;

        for (int i=0; i < M.length; i++) {
            if (!visited[i]) {
                dfs(i);
                count++;
            }
        }
        return count;
    }

    private void dfs(int i) {
        for (int j=0; j < M.length; j++) {
            if (M[i][j] == 1 && !visited[j]) {
                visited[j] = true;
                dfs(j);
            }
        }
    }
}
```

# 并查集

```python
class Solution:
    def findCircleNum(self, M):
        if not M: return 0

        n = len(M)
        p = [i for i in range(n)]

        for i in range(n):
            for j in range(n):
                if M[i][j] == 1:
                    self._union(p, i, j)

        return len(set([self._parent(p, i) for i in range(n)]))

    def _union(self, p, i, j):
        p1 = self._parent(p, i)
        p2 = self._parent(p, j)

        p[p2] = p1

    def _parent(self, p, i):
        root = i
        while p[root] != root:
            root = p[root]

        while p[i] != i:
            x = i
            i = p[i]
            p[x] = root

        return root
```
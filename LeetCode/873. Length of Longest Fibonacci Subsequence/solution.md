```java
class Solution {
    public int lenLongestFibSubseq(int[] A) {
        Set<Integer> s = new HashSet<>();
        for (int x : A) s.add(x);
        int res = 2;
        for (int i = 0; i < A.length; ++i)
            for (int j = i + 1; j < A.length; ++j) {
                int a = A[i], b = A[j], l = 2;
                while (s.contains(a + b)) {
                    b = a + b;
                    a = b - a;
                    l++;
                }
                res = Math.max(res, l);
            }
        return res > 2 ? res : 0;
    }
}
```


# 动态规划

将斐波那契式的子序列中的两个连续项 `A[i]`, `A[j]` 视为单个结点 `(i, j)`，整个子序列是这些连续结点之间的路径。
> 例如，对于斐波那契式的子序列 `(A[1] = 2, A[2] = 3, A[4] = 5, A[7] = 8, A[10] = 13)`，结点之间的路径为 `(1, 2) <-> (2, 4) <-> (4, 7) <-> (7, 10)`。

这样做的动机是，只有当 `A[i] + A[j] == A[k]` 时，两结点 `(i, j)` 和 `(j, k)` 才是连通的，我们需要这些信息才能知道这一连通。现在我们得到一个类似于 最长上升子序列 (Leetcode 300) 的问题。

设 `longest[i, j]` 是结束在 `[i, j]` 的最长路径。那么 如果 `(i, j)` 和 `(j, k)` 是连通的， `longest[j, k] = longest[i, j] + 1`。


由于 `i` 由 `A.index(A[k] - A[j])` 唯一确定，所以这是有效的：我们在 `i` 潜在时检查每组 `j < k`，并相应地更新 `longest[j, k]`。


```java
class Solution {
    public int lenLongestFibSubseq(int[] A) {
        int N = A.length;
        Map<Integer, Integer> index = new HashMap();
        for (int i = 0; i < N; ++i)
            index.put(A[i], i);

        Map<Integer, Integer> longest = new HashMap();
        int ans = 0;

        for (int k = 0; k < N; ++k)
            for (int j = 0; j < k; ++j) {
                int i = index.getOrDefault(A[k] - A[j], -1);
                if (i >= 0 && i < j) {
                    // Encoding tuple (i, j) as integer (i * N + j)
                    int cand = longest.getOrDefault(i * N + j, 2) + 1;
                    longest.put(j * N + k, cand);
                    ans = Math.max(ans, cand);
                }
            }

        return ans >= 3 ? ans : 0;
    }
}
```
动态规划

```java
class Solution {
    private int[][] opt;

    public int uniquePaths(int m, int n) {
        opt = new int[m+1][n+1];
        for (int i = m-1; i >=0 ; i--) {
            for (int j = n-1; j >=0 ; j--) {
                if (i == m-1 && j == n-1)
                    opt[i][j] = 1;
                else
                    opt[i][j] = opt[i][j+1] + opt[i+1][j];
            }
        }
        return opt[0][0];
    }
}
```
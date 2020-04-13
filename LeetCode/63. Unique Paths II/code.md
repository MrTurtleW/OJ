```java
class Solution {

    private int[][] obstacleGrid;

    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        this.obstacleGrid = obstacleGrid;
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] opt = new int[m + 1][n + 1];
        for (int i = m-1; i >=0 ; i--) {
            for (int j = n-1; j >=0 ; j--) {
                if (!isValid(i, j))
                    continue;;
                if (i == m-1 && j == n-1)
                    opt[i][j] = 1;
                else
                    opt[i][j] = opt[i][j+1] + opt[i+1][j];
            }
        }
        return opt[0][0];
    }

    private boolean isValid(int i, int j) {
        return obstacleGrid[i][j] == 0;
    }
}
```
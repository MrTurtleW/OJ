```java
class Solution {
    public int minPathSum(int[][] grid) {
        if (grid.length == 0 || grid[0].length == 0)
            return 0;

        int[][] distance = new int[grid.length][grid[0].length];

        distance[0][0] = grid[0][0];
        for (int i = 1; i < grid[0].length; i++)
            distance[0][i] = distance[0][i-1] + grid[0][i];

        for (int i = 1; i < grid.length; i++)
            distance[i][0] = distance[i-1][0] + grid[i][0];

        for (int i = 1; i < grid.length; i++) {
            for (int j = 1; j < grid[0].length; j++) {
                distance[i][j] = Math.min(distance[i][j-1], distance[i-1][j]) + grid[i][j];
            }
        }
        return distance[grid.length-1][grid[0].length-1];
    }
}
```


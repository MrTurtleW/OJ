# DFS

```java
class Solution {
    private char[][] grid;
    private boolean[][] visited;

    public int numIslands(char[][] grid) {
        int count = 0;

        if (grid.length == 0 || grid[0].length == 0)
            return count;

        this.grid = grid;
        this.visited = new boolean[grid.length][grid[0].length];
        for (int i=0; i< grid.length; i++) {
            for (int j=0; j < grid[0].length; j++) {
                if (!visited[i][j] && grid[i][j] == '1') {
                    dfs(i, j);
                    count++;
                }
            }
        }
        return count;
    }

    private void dfs(int i, int j) {
        if (grid[i][j] == '0')
            return;

        if (visited[i][j])
            return;

        visited[i][j] = true;
        if (i < grid.length -  1)
            dfs(i+1, j);
        if (j < grid[0].length - 1)
            dfs(i, j+1);

        if (i > 0)
            dfs(i-1, j);
        if (j > 0)
            dfs(i, j-1);
    }

    public static void main(String[] args) {
        char[][] grid = {
                "111".toCharArray(),
                "010".toCharArray(),
                "111".toCharArray()
        };

        Solution solution = new Solution();
        System.out.println(solution.numIslands(grid));
    }
}
```
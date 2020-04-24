解题思路：
1. 查找所有边界，找到所有的O，然后设为1
2. 再把所有的O为X
3. 然后把1改为O

```java
class Solution {
    private char[][] board;
    private boolean[][] visited;
    public void solve(char[][] board) {
        this.board = board;

        if (board.length == 0 || board[0].length == 0)
            return;

        visited = new boolean[board.length][board[0].length];

        for (int i = 0; i < board.length; i++) {
            if (board[i][0] == 'O')
                dfs(i, 0);

            if (board[i][board[0].length-1] == 'O')
                dfs(i, board[0].length-1);
        }

        for (int i = 0; i < board[0].length; i++) {
            if (board[0][i] == 'O')
                dfs(0, i);
            if (board[board.length-1][i] == 'O')
                dfs(board.length-1, i);
        }

        for (int i=0; i<board.length; i++){
            for (int j=0; j<board[0].length; j++) {
                if (board[i][j] == 'O')
                    board[i][j] = 'X';
            }
        }
        for (int i=0; i<board.length; i++){
            for (int j=0; j<board[0].length; j++) {
                if (board[i][j] == '1')
                    board[i][j] = 'O';
            }
        }
    }

    private void dfs(int i, int j) {
        if (board[i][j] == 'X' || visited[i][j])
            return;

        visited[i][j] = true;
        board[i][j] = '1';
        if (i < board.length-1)
            dfs(i+1, j);
        if (i > 0)
            dfs(i-1, j);

        if (j < board[0].length-1)
            dfs(i, j+1);
        if (j > 0)
            dfs(i, j-1);
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        char[][] board = {
                "XXXX".toCharArray(),
                "XOOX".toCharArray(),
                "XXOX".toCharArray(),
                "XOXX".toCharArray()
        };
        solution.solve(board);
        for (int i = 0; i < board.length; i++) {
            System.out.println(new String( board[i]));
        }
    }
}
```
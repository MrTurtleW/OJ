```java
class Solution {

    private char[][] board;
    private String word;

    private boolean[][] used;
    public boolean exist(char[][] board, String word) {
        if (board == null || board.length == 0 || board[0].length == 0 || word.length() == 0)
            return false;

        this.board = board;
        this.word = word;

        used = new boolean[board.length][board[0].length];

        for (int i = 0; i< board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (board[i][j] == word.charAt(0)) {
                    used[i][j] = true;
                    if (helper(0, i, j))
                        return true;
                    used[i][j] = false;
                }
            }
        }
        return false;
    }

    private boolean helper(int index, int i, int j) {
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || index >= word.length())
            return false;

        if (board[i][j] != word.charAt(index))
            return false;

        if (index == word.length() - 1)
            return true;

        if (i > 0 && !used[i-1][j]) {
            used[i-1][j] = true;
            if (helper(index+1, i-1, j))
                return true;
            used[i-1][j] = false;

        }

        if (i < board.length - 1 && !used[i+1][j]) {
            used[i+1][j] = true;
            if (helper(index+1, i+1, j))
                return true;
            used[i+1][j] = false;
        }

        if (j > 0 && !used[i][j-1]) {
            used[i][j-1] = true;
            if (helper(index+1, i, j-1))
                return true;
            used[i][j-1] = false;

        }

        if (j < board[0].length - 1 && !used[i][j+1]) {
            used[i][j+1] = true;
            if (helper(index+1, i, j+1))
                return true;
            used[i][j+1] = false;
        }

        return false;
    }
}
```


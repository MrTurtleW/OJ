```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        if (!checkRow(board))
            return false;
        if (!checkColumn(board))
            return false;
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (!checkCell(board, i, j))
                        return false;
            }
        }
        return true;
    }

    private boolean checkRow(char[][] board) {
        for (char[] rows : board) {
            Map<Character, Integer> map = new HashMap<>();
            for (char c: rows) {
                if (c != '.') {
                    if (map.containsKey(c))
                        return false;
                    map.put(c, 1);
                }
            }
        }
        return true;
    }

    private boolean checkColumn(char[][] board) {
        for (int i = 0; i < 9; i++) {
            Map<Character, Integer> map = new HashMap<>();
            for (int j = 0; j < 9; j++) {
                if (board[j][i] != '.') {
                    if (map.containsKey(board[j][i]))
                        return false;
                    map.put(board[j][i], 1);
                }
            }
        }
        return true;
    }

    private boolean checkCell(char[][] board, int i, int j) {
        Map<Character, Integer> map = new HashMap<>();
        for (int k = 0; k < 3; k++) {
            for (int l = 0; l < 3; l++) {
                if (board[3*i+k][3*j+l] != '.') {
                    if (map.containsKey(board[i*3+k][j*3+l]))
                        return false;
                    map.put(board[i*3+k][j*3+l], 1);
                }
            }
        }
        return true;
    }
}
```
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0)
            return false;

        if (target < matrix[0][0] || target > matrix[matrix.length-1][matrix[0].length-1])
            return false;

        int startRow = 0, endRow = matrix.length - 1, midRow = 0;

        while (startRow <= endRow) {
            midRow = (endRow + startRow) / 2;

            if (matrix[midRow][0] < target) {
                if (midRow == matrix.length - 1 || matrix[midRow+1][0] > target)
                    break;
                startRow = midRow + 1;
            }
            else if (matrix[midRow][0] > target) {
                endRow = midRow - 1;
            }
            else if (matrix[midRow][0] == target)
                return true;
        }

        int startCol = 0, endCol = matrix[0].length - 1;

        while (startCol <= endCol) {
            int midCol = (startCol + endCol) / 2;
            if (matrix[midRow][midCol] < target)
                startCol = midCol + 1;
            else if (matrix[midRow][midCol] > target) {
                endCol = midCol - 1;
            }
            else if (matrix[midRow][midCol] == target)
                return true;
        }
        return false;
    }
}
```


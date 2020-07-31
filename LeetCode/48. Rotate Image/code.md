```java
class Solution {
    public void rotate(int[][] matrix) {
        if (matrix.length == 0 || matrix[0].length == 0)
            return;
        for (int i = 0; i < matrix.length / 2; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[matrix.length-i-1][j];
                matrix[matrix.length-i-1][j] = temp;
            }
        }

        for (int i = 0; i < matrix.length; i++) {
            for (int j = i+1; j < matrix[0].length; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
    }
}
```


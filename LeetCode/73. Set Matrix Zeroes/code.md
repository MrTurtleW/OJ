```java
class Solution {
    private int[][] matrix;
    private Set<Integer> rows = new HashSet<>();
    private Set<Integer> cols = new HashSet<>();
    public void setZeroes(int[][] matrix) {
        this.matrix = matrix;

        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (matrix[i][j] == 0) {
                    rows.add(i);
                    cols.add(j);
                }
            }
        }

        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (rows.contains(i) || cols.contains(j))
                   matrix[i][j] = 0;
            }
        }
    }
}
```


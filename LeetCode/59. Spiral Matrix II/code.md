```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] result = new int[n][n];
        if (n <= 0)
            return result;
        int left = 0, up = 0, right = n - 1, down = n - 1;
        int count = 0;
        while (count < n * n) {
            for (int i = left; i <= right && count < n * n; i++)
                result[up][i] = ++count;

            for (int i = up + 1; i <= right && count < n * n; i++)
                result[i][right] = ++count;

            for (int i = right - 1; i >= left && count < n * n; i--)
                result[down][i] = ++count;

            for (int i = down - 1; i >= up + 1 && count < n * n; i--)
                result[i][left] = ++count;

            left++; up++; right--; down--;
        }

        return result;
    }

}
```


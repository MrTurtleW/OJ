```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int[][] c = new int[text1.length()+1][text2.length()+1];
        int m = text1.length();
        int n = text2.length();
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1.charAt(i-1) == text2.charAt(j-1))
                    c[i][j] = c[i-1][j-1] + 1;
                else
                    c[i][j] = Math.max(c[i-1][j], c[i][j-1]);
            }
        }
        
        return c[m][n];
    }
}
```
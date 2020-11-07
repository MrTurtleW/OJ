# DP

```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s3.length() != s1.length() + s2.length())
            return false;

        boolean[][] table = new boolean[s1.length()+1][s2.length()+1];

        table[0][0] = true;

        for (int i=1; i <= s1.length(); i++) {
            table[i][0] = table[i-1][0] && s1.charAt(i-1) == s3.charAt(i-1);
        }

        for (int i=1; i <= s2.length(); i++) {
            table[0][i] = table[0][i-1] && s2.charAt(i-1) == s3.charAt(i-1);
        }

        for (int i=1; i <= s1.length(); i++) {
            for (int j=1; j <= s2.length(); j++) {
                table[i][j] = (table[i-1][j] && s1.charAt(i-1) == s3.charAt(i+j-1)) || (table[i][j-1] && s2.charAt(j-1) == s3.charAt(i+j-1));
            }
        }
        return table[s1.length()][s2.length()];
    }
}
```


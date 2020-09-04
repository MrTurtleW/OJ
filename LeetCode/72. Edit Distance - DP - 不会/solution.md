We define the state `dp[i][j]` to be the minimum number of operations to convert `word1[0...i)` to `word2[0...j)`

- For the base case, that is, to convert a string to an empty string, the minimum number of operations(deletions) is just the length of the string. So we have `dp[i][0] = i`, `dp[0][j] = j`

- For the general case to convert `word1[0...i)` to `word2[0...j)`, we break this problem down into sub-problems. Suppose we have already known how to convert `word1[0...i-1)` to `word2[0...j-1)`, if `word1[i-1] = word2[j-1]`, then no more operation is needed and `dp[i][j] = dp[i-1][j-1]`

- If `word1[i-1] != word2[j-1]`, we need to consider three cases

  - Replace `word1[i-1]` by `word2[j-1] `(`dp[i][j] = dp[i-1][j-1] + 1`)
  - If `word1[0...j-1) = word2[0...j)`, then **delete** `word1[i-1]` (`dp[i][j] = dp[i-1][j] + 1`)
  -   If `word1[0...j-1) + word2[j-1] = word2[0..j)`, then **insert** `word2[j-1]` to `word1[0...j)` (`dp[i][j] = dp[i][j-1] + 1 `)

  So when `word1[i-1] != word2[j-1]`, `dp[i][j]` will just be the minimum of the above three cases.

```java
class Solution {
    public int minDistance(String word1, String word2) {
        if((word1.length() == 0 && word2.length() == 0) || word1.equals(word2))
            return 0;
        int[][] dp = new int[word1.length()+1][word2.length()+1];

        for (int i = 1; i <= word1.length(); i++)
            dp[i][0] = i;

        for (int j = 1; j <= word2.length(); j++)
            dp[0][j] = j;

        for (int i = 1; i <= word1.length(); i++) {
            for (int j = 1; j <= word2.length(); j++) {
                if (word1.charAt(i-1) == word2.charAt(j-1))
                    dp[i][j] = dp[i-1][j-1];
                else
                    dp[i][j] = Math.min(dp[i-1][j-1], Math.min(dp[i-1][j], dp[i][j-1])) + 1;
            }
        }

        return dp[word1.length()][word2.length()];
    }
}
```


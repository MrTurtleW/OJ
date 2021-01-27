# DP

```c++
class Solution {
public:
    string longestPalindrome(string s) {
        vector<vector<bool>> dp(s.length(), vector<bool>(s.length()));
        string res = "";

        // dp[i][j] = true if s[i] = s[j] and s[i+1 ...j-1] is a palindromic substring
        for (int i = s.length()-1; i >= 0; i--) {
            for (int j = i; j < s.length(); j++) {
                dp[i][j] = s[i] == s[j] && (j - i < 3 || dp[i + 1][j - 1]);

                if (dp[i][j] && j - i + 1 > res.length()) {
                    res = s.substr(i, j - i + 1);
                }
            }
        }

        return res;
    }
};
```


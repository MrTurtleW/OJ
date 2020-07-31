超时：

```java
class Solution {
    public boolean isMatch(String s, String p) {
        if (p.length() == 0 && s.length() == 0)
            return true;
        if (p.length() == 0)
            return false;
        return helper(s, p, 0, 0);
    }

    private boolean helper(String s, String p, int sIndex, int pIndex) {
        if (pIndex == p.length() && sIndex == s.length())
            return true;

        if (pIndex >= p.length() || sIndex > s.length())
            return false;

        if (p.charAt(pIndex) == '*') {
            while (pIndex + 1 < p.length() && p.charAt(pIndex+1) == '*')
                pIndex++;

            // 匹配空
            if (helper(s, p, sIndex, pIndex+1))
                return true;
            // 匹配一个
            if (helper(s, p, sIndex+1, pIndex+1))
                return true;
            // 匹配多个字符
            return helper(s, p, sIndex + 1, pIndex);
        }

        if (sIndex >= s.length())
            return false;

        if (p.charAt(pIndex) == s.charAt(sIndex) || p.charAt(pIndex) == '?')
            return helper(s, p, sIndex+1, pIndex+1);

        return false;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.isMatch("babbbbaabababaabbababaababaabbaabababbaaababbababaaaaaabbabaaaabababbabbababbbaaaababbbabbbbbbbbbbaabbb"
                ,"b**bb**a**bba*b**a*bbb**aba***babbb*aa****aabb*bbb***a"));
    }
}
```

动态规划：

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        m = len(s)
        n = len(p)

        dp = [[False for i in range(n+1)] for j in range(m+1)]
        dp[0][0] = True

        for i in range(n):
            if p[i] == '*':
                dp[0][i+1] = True
            else:
                break

        for i in range(m):
            for j in range(n):
                if p[j] == '*':
                    dp[i+1][j+1] = dp[i+1][j] or dp[i][j+1]
                elif p[j] == '?' or p[j] == s[i]:
                    dp[i+1][j+1] = dp[i][j]
                    
        return dp[m][n]
```


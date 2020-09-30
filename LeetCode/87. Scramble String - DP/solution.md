# 递归

```java
class Solution {
    public boolean isScramble(String s1, String s2) {
        if (s1.equals(s2))
            return true;

        int[] count = new int[26];

        for (int i = 0; i < s1.length(); i++) {
            count[s1.charAt(i) - 'a'] ++;
            count[s2.charAt(i) - 'a'] --;
        }

        for (int i : count) {
            if (i != 0)
                return false;
        }
        for (int i = 1; i < s1.length(); i++) {
            if (isScramble(s1.substring(0, i), s2.substring(0, i)) && isScramble(s1.substring(i), s2.substring(i)))
                return true;
            if (isScramble(s1.substring(0, i), s2.substring(s1.length()-i)) && isScramble(s1.substring(i), s2.substring(0, s1.length()-i)))
                return true;
        }
        return false;
    }
}
```

假设长度为$n$的字符串的时间复杂度为$T(n)$，则`isScramble(s1.substring(0, i), s2.substring(0, i)) && isScramble(s1.substring(i), s2.substring(i))`需要的时间复杂度为$T(i)+T(n-i)$，下面的递归调用相同，也是$T(i)+T(n-i)$，于是有
$$
\begin{aligned}
T(n)&=\sum_{i=1}^{n-1}2 *(T(i)+T(n-i))\\
&=2*(T(1)+T(n-1)+T(2)+T(n-2)+\cdots+T(n-1)+T(1))\\
&=4*(T(1)+T(2)+\cdots+T(n-1))
\end{aligned}
$$
如果把$n$替换为$n-1$，有
$$
T(n-1)=4*(T(1)+T(2)+\cdots+T(n-2))
$$
所以
$$
\begin{aligned}
T(n)&=4*(T(1)+T(2)+\cdots+T(n-1))\\
&=4*(T(1)+T(2)+\cdots+T(n-2))+4*T(n-1)\\
&=5*T(n-1)\\
&=5*5*T(n-2)\\
&...\\
&=O(5^n)
\end{aligned}
$$
不使用`substring`能提高性能：

```java
class Solution {
    public boolean isScramble(String s1, String s2) {
        if (s1.length() != s2.length()) return false;
        if (s1.isEmpty()) return true;
        if (s1.equals(s2)) return true;
        return isScramble(s1, s2, 0, 0, s1.length());
    }

    public boolean permutation(String s1, String s2, int i1, int i2, int n) {
        int[] cs = new int[26];
        for (int i = 0; i < n; i++) {
            cs[s1.charAt(i1+i)-'a']++;
            cs[s2.charAt(i2+i)-'a']--;
        }
        for (int m : cs) if (m != 0) return false;
        return true;
    }

    public boolean equal(String s1, String s2, int i1, int i2, int n) {
        for (int i = 0; i < n; i++) {
            if (s1.charAt(i1+i) != s2.charAt(i2+i)) return false;
        }
        return true;
    }

    public boolean isScramble(String s1, String s2, int i1, int i2, int n) {
        if (equal(s1,s2,i1,i2,n)) return true;
        if (!permutation(s1,s2,i1,i2,n)) return false;
        for (int len=1; len<n; len++) {
            if (isScramble(s1, s2, i1, i2, len) && isScramble(s1, s2, i1+len, i2+len, n-len)) return true;
            if (isScramble(s1, s2, i1, i2+n-len, len) && isScramble(s1, s2, i1+len, i2, n-len)) return true;
        }
        return false;
    }
}
```

# DP

`dp[i][j][len]`表示从字符串$S$中$i$开始长度为$len$的字符串是否能变换为字符串$T$中$j$开始长度为$len$的字符串，所以答案是`dp[0][0][n]`

```java
class Solution {
    public boolean isScramble(String s1, String s2) {
        if (s1.length() != s2.length())
            return false;

        boolean[][][] dp = new boolean[s1.length()][s1.length()][s1.length()+1];

        // 初始化单个字符的情况
        for (int i = 0; i < s1.length(); i++) {
            for (int j = 0; j < s2.length(); j++) {
                dp[i][j][1] = s1.charAt(i) == s2.charAt(j);
            }
        }

        // 枚举区间长度 2-n
        for (int len = 2; len <= s1.length(); len++) {
            // 枚举S中的起点位置
            for (int i = 0; i <= s1.length() - len; i++) {
                // 枚举T中的起点位置
                for (int j = 0; j <= s1.length() - len; j++) {
                    // 枚举划分位置
                    for (int k = 1; k <= len - 1; k++) {
                        // 第一种情况 S1 -> T1, S2 -> T2
                        if (dp[i][j][k] && dp[i+k][j+k][len-k]) {
                            dp[i][j][len] = true;
                            break;
                        }
                        
                        // 第二种情况：S1 -> T2, S2 -> T1
                        if (dp[i][j+len-k][k] && dp[i+k][j][len-k]) {
                            dp[i][j][len] = true;
                            break;
                        }
                    }
                }
            }
        }
        return dp[0][0][s1.length()];
    }
}
```


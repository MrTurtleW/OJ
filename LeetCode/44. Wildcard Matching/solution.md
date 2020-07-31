# 动态规划（72s）：

在给定的模式p中，只会有三种类型的字符出现：
- 小写字母`a-z`，可以匹配对应的一个小写字母
- 问号`?`，可以匹配任意一个小写字母
- 型号`*`，可以匹配任意字符串。

我们用`dp[i][j]`表示字符串$s$的前$i$各字符和模式$p$的前$j$个字符是否能匹配。在进行状态转移时，我们可以考虑模式$p$的第$j$个字符$p_j$，与之对应的是字符串$s$中的第$i$个字符$s_i$
- 如果$p_j$是字母，那么$s_i$也必须为相同的小写字母

    $$
    dp[i][j] = s_i==p_j \cap dp[i-1][j-1]
    $$
    
    
- 如果$p_j$为问号，$s_i$没有要求

    $$
    dp[i][j] = dp[i-1][j-1]
    $$
    
    
- 如果$p_j$是问号，那么对$s_i$没有任何要求，状态转移方程为

    $$
    dp[i][j] = dp[i-1][j] 	\cup dp[i][j-1]
    $$
    

归纳得状态转移方程：

$$
dp[i][j] = \begin{cases}
dp[i-1][j-1],&s_i=p_j或者p_j=?\\
dp[i][j-1]\cup dp[i-1][j],&p_j=*\\
False, &其他
\end{cases}
$$


边界条件：
- `dp[0][0]=True`
- `dp[i][0]=False`
- `dp[0][j]`需要分情况讨论，因为星号才能匹配字符串，所以只有当模式$p$的前$j$个字符均为星号时，`dp[0][j]`才为真。



```java
class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length();
        int n = p.length();
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;
        for (int i = 1; i <= n; ++i) {
            if (p.charAt(i - 1) == '*') {
                dp[0][i] = true;
            } else {
                break;
            }
        }
        for (int i = 1; i <= m; ++i) {
            for (int j = 1; j <= n; ++j) {
                if (p.charAt(j - 1) == '*') {
                    dp[i][j] = dp[i][j - 1] || dp[i - 1][j];
                } else if (p.charAt(j - 1) == '?' || s.charAt(i - 1) == p.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                }
            }
        }
        return dp[m][n];
    }
}
```

# 贪心算法 4ms：

动态规划的瓶颈在于对星号`*`的处理方式：使用动态规划枚举所有情况。由于星号是万能的匹配字符，连续的多个星号和单个星号实际上是等价的，那么不连续的多个星号呢？

我们以`p=*abcd*`为例，$p$可以匹配所有包含子串`abcd`的字符串。也就是说，我们只需要暴力地枚举字符串s中的每个位置作为起始位置，并判断对应的子串是否为abcd即可。这种暴力方法的时间复杂度为$O(mn)$，与动态规划一致，但不需要额外的空间。

如果`p=*abcd*efgh*i*`呢？显然，$p$可以匹配所有依次出现子串`abcd`、`efgh`、`i`的字符串。此时，对于任意一个字符串$s$，我们先暴力找到最早出现的`abcd`，随后从下一位置开始暴力找到最早出现的`efgh`，最后找出`i`，就可以判断`s`是否与`p`匹配。

因此，如果模式`p`的形式是$*u_1*u_2*u_3*\cdots*u_x*$，即字符串（可以为空）和星号交替出现，并且首尾字母均为星号，那么我们就可以设计出下面这个基于贪心的暴力匹配算法。算法的本质是：如果在字符串$s$中首先找到$u_1$，再找到$u_2,u_3,\cdots,u_x$，那么$s$就可以与模式$p$匹配。

```python
# 我们用 sIndex 和 pIndex 表示当前遍历到 s 和 p 的位置
# 此时我们正在 s 中寻找某个 u_i
# 其在 s 和 p 中的起始位置为 sRecord 和 pRecord

# sIndex 和 sRecord 的初始值为 0
# 即我们从字符串 s 的首位开始匹配
sIndex = sRecord = 0

# pIndex 和 pRecord 的初始值为 1
# 这是因为模式 p 的首位是星号，那么 u_1 的起始位置为 1
pIndex = pRecord = 1

while sIndex < s.length and pIndex < p.length do
    if p[pIndex] == '*' then
        # 如果遇到星号，说明找到了 u_i，开始寻找 u_i+1
        pIndex += 1
        // 记录下起始位置
        sRecord = sIndex
        pRecord = pIndex
    else if match(s[sIndex], p[pIndex]) then
        # 如果两个字符可以匹配，就继续寻找 u_i 的下一个字符
        sIndex += 1
        pIndex += 1
    else if sRecord + 1 < s.length then
        # 如果两个字符不匹配，那么需要重新寻找 u_i
        # 枚举下一个 s 中的起始位置
        sRecord += 1
        sIndex = sRecord
        pIndex = pRecord
    else
        # 如果不匹配并且下一个起始位置不存在，那么匹配失败
        return False
    end if
end while

# 由于 p 的最后一个字符是星号，那么 s 未匹配完，那么没有关系
# 但如果 p 没有匹配完，那么 p 剩余的字符必须都是星号
return all(p[pIndex] ~ p[p.length - 1] == '*')
```

然而模式$p$并不一定是$*u_1*u_2*u_3*\cdots*u_x*$的形式：
- 模式$p$的开头字符不是星号
- 模式$p$的结尾字符不是星号。

如果模式$p$的结尾字符不是星号，那么就必须与字符串$s$的结尾字符匹配。那么我们不断地匹配$s$和$p$地结尾字符，直到$p$为空或者$p$的结尾字符为星号为止。在这个过程中，如果匹配失败，或者最后$p$为空但$s$不为空，那么需要返回False

第一种情况的处理也很类似，我们可以不断地匹配 $s$ 和 $p$ 的开头字符。下面的代码中给出了另一种处理方法，即修改 $\textit{sRecord}$ 和 $\textit{tRecord}$ 的初始值为 −1，表示模式 p 的开头字符不是星号，并且在匹配失败时进行判断，如果它们的值仍然为 -1，说明没有「反悔」重新进行匹配的机会。


```java
class Solution {
    public boolean isMatch(String s, String p) {
        int sRight = s.length(), pRight = p.length();
        while (sRight > 0 && pRight > 0 && p.charAt(pRight - 1) != '*') {
            if (charMatch(s.charAt(sRight - 1), p.charAt(pRight - 1))) {
                --sRight;
                --pRight;
            } else {
                return false;
            }
        }

        if (pRight == 0) {
            return sRight == 0;
        }

        int sIndex = 0, pIndex = 0;
        int sRecord = -1, pRecord = -1;
        
        while (sIndex < sRight && pIndex < pRight) {
            if (p.charAt(pIndex) == '*') {
                ++pIndex;
                sRecord = sIndex;
                pRecord = pIndex;
            } else if (charMatch(s.charAt(sIndex), p.charAt(pIndex))) {
                ++sIndex;
                ++pIndex;
            } else if (sRecord != -1 && sRecord + 1 < sRight) {
                ++sRecord;
                sIndex = sRecord;
                pIndex = pRecord;
            } else {
                return false;
            }
        }

        return allStars(p, pIndex, pRight);
    }

    public boolean allStars(String str, int left, int right) {
        for (int i = left; i < right; ++i) {
            if (str.charAt(i) != '*') {
                return false;
            }
        }
        return true;
    }

    public boolean charMatch(char u, char v) {
        return u == v || v == '?';
    }
}
```
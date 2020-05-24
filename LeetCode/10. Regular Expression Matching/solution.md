# 递归

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        if len(p) <= 0:
            return len(s) <= 0

        match = len(s) > 0 and (s[0] == p[0] or p[0] == '.')
        if len(p) > 1 and p[1] == '*':
            return self.isMatch(s, p[2:]) or (match and self.isMatch(s[1:], p))
        else:
            return match and self.isMatch(s[1:],p[1:])
```

# 动态规划

使用 `match(i,j)` 表示`s[i:]`与`p[j:]`的匹配情况，如果能匹配，则置为true，否则置为false。这就是各个子问题的状态。

对于`match(i, j)`的值，取决于`p[j+1]`是否为`*`：`currMatch = i < len(s) and (s[i] == p[j] or p[j] == '.')`
- if `p[j+1] != '*'`， `match(i, j)=currMatch and match(i+1, j+1)`
- if `p[j+1] == '*'`， `match[i, j] = match(i, j+2) or (currMatch and match(i+1, j)`

https://www.cnblogs.com/mfrank/p/10472663.html
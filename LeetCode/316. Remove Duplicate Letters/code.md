超时：

```python
class Solution:
    def __init__(self):
        self.s = None
        self.res = None
        self.count = {}

    def removeDuplicateLetters(self, s: str) -> str:
        self.s = s
        for ch in s:
            self.count[ch] = self.count.get(ch, 0) + 1

        self.dfs("", 0)
        return self.res

    def dfs(self, res, index):
        if len(res) == len(self.count):
            if self.res is None or res < self.res:
                self.res = res

            return

        self.count[self.s[index]] -= 1

        if self.s[index] in res:
            self.dfs(res, index + 1)

        elif self.count[self.s[index]] == 0:
            self.dfs(res + self.s[index], index + 1)
        else:
            self.dfs(res, index + 1)
            self.dfs(res + self.s[index], index + 1)

        self.count[self.s[index]] += 1
```


```python
class Solution:
    def __init__(self):
        self._res = []
        self._candidates = None

    def combinationSum(self, candidates, target):
        self._candidates = candidates
        # increasing order
        self._candidates.sort()
        self._dfs(target, [], 0)
        return self._res

    def _dfs(self, target, combination, begin):
        if target < 0:
            return

        if target == 0:
            self._res.append(combination)
            return

        for index in range(begin, len(self._candidates)):
            # since it's in increasing order, we can break it
            if target < self._candidates[index]:
                break
            self._dfs(target - self._candidates[index], combination + [self._candidates[index]], index)

if __name__ == '__main__':
    solution = Solution()
    print(solution.combinationSum([5, 2, 3], 8))
```

不排序也可以

```python
class Solution:
    def __init__(self):
        self._res = []
        self._candidates = None

    def combinationSum(self, candidates, target):
        self._candidates = candidates
        self._dfs(target, [], 0)
        return self._res

    def _dfs(self, target, combination, begin):
        if target < 0:
            return

        if target == 0:
            self._res.append(combination)
            return

        for index in range(begin, len(self._candidates)):
            self._dfs(target - self._candidates[index], combination + [self._candidates[index]], index)

if __name__ == '__main__':
    solution = Solution()
    print(solution.combinationSum([5, 2, 3], 8))
```
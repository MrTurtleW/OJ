```python
from typing import List


class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        self.n = n
        self.res = []
        self.helper([], [], [])
        return self.res

    def helper(self, queues, xySum, xySub):
        if len(queues) == self.n:
            tempRes = []
            for i in range(self.n):
                tempRes.append("")
                for j in range(self.n):
                    if queues[i] == j:
                        tempRes[i] += 'Q'
                    else:
                        tempRes[i] += '.'

            self.res.append(tempRes)
            return

        current_row = len(queues)
        for i in range(self.n):
            if i not in queues and current_row + i not in xySum and current_row - i not in xySub:
                self.helper(queues + [i], xySum + [current_row + i], xySub + [current_row - i])

if __name__ == '__main__':
    solution = Solution()
    print(solution.solveNQueens(4))
```
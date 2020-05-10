# 2020-04-28

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [-1 for i in range(amount + 1)]
        _sum = 1
        dp[0] = 0

        while _sum <= amount:
            _min = sys.maxsize
            for coin in coins:
                if _sum >= coin and dp[_sum - coin] != -1 and dp[_sum - coin] + 1 < _min:
                    _min = dp[_sum - coin] + 1

            if _min == sys.maxsize:
                dp[_sum] = -1
            else:
                dp[_sum] = _min

            _sum += 1

        return dp[amount]
```
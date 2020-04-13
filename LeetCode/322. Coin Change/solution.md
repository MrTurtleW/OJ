Suppose we have already found out the best way to sum up to amount `a`, then for last step, we can choose any coin type which gives us a remainder `r` where `r=a-coins[i]` for all `i`'s

```java
class Solution {

    private int[] coins;
    // count[rem]: minimum number of coins to sum up to rem
    private int[] count;
    public int coinChange(int[] coins, int amount) {
        this.coins = coins;
        this.count = new int[amount];
        return helper(amount);
    }

    private int helper(int remainder) {
        if (remainder < 0) return -1;
        if (remainder == 0) return 0;
        if (count[remainder-1] != 0) return count[remainder-1];
        
        int min = Integer.MAX_VALUE;
        for(int coin: coins) {
            int res = helper(remainder-coin);
            if (res >= 0 && res < min)
                min = res + 1;
        }
        count[remainder-1] = (min == Integer.MAX_VALUE) ? -1 : min;
        return count[remainder-1];
    }
}
```

从小到大依次计算：
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        
        int sum = 0;
        int[] dp = new int[amount+1];
        while(++sum <= amount) {
            int min = Integer.MAX_VALUE;
            for(int coin: coins) {
                if (sum >= coin && dp[sum-coin] != -1) {
                    int temp = dp[sum-coin] +1;
                    if (temp < min)
                        min = temp;
                }
            }
            if (min == Integer.MAX_VALUE)
                dp[sum] = -1;
            else
                dp[sum] = min;
        }
        return dp[amount];
    }
}
```
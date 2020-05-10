```java
class Solution {
    public int maxProduct(int[] nums) {
        Tuple[] dp = new Tuple[nums.length];
        dp[0] = new Tuple(nums[0],nums[0]);
        int res = dp[0].imax;
        for (int i = 1; i < nums.length; i++) {
            Tuple prev = dp[i - 1];
            int imax = Math.max(Math.max(nums[i], nums[i] * prev.imax) , nums[i] * prev.imin);
            int imin = Math.min(Math.min(nums[i], nums[i] * prev.imax) , nums[i] * prev.imin);
            dp[i] = new Tuple(imax,imin);
            res = Math.max(imax, res);
        }
        return res;
    }

    class Tuple {
        private int imax;
        private int imin;
        private Tuple(int imax, int imin) {
            this.imax = imax;
            this.imin = imin;
        }
    }
}
```

更简洁:dp数组的原因是`dp[i]`只依赖于`dp[i - 1]`因此没有必要把前面所有的信息都存起来，只需要存前一个`dp[i-1]`的最大和最小的乘积就可以了。

```c++
int maxProduct(int A[], int n) {
    // store the result that is the max we have found so far
    int r = A[0];

    // imax/imin stores the max/min product of
    // subarray that ends with the current number A[i]
    for (int i = 1, imax = r, imin = r; i < n; i++) {
        // multiplied by a negative makes big number smaller, small number bigger
        // so we redefine the extremums by swapping them
        if (A[i] < 0)
            swap(imax, imin);

        // max/min product for the current number is either the current number itself
        // or the max/min by the previous number times the current one
        imax = max(A[i], imax * A[i]);
        imin = min(A[i], imin * A[i]);

        // the newly computed max value is a candidate for our global result
        r = max(r, imax);
    }
    return r;
}
```
分治法：

```java
class Solution {
    private int[] nums;
    public int maxSubArray(int[] nums) {
        this.nums = nums;
        return helper(0, nums.length-1);
    }

    private int helper(int start, int end) {
        if (start > end)
            return Integer.MIN_VALUE;

        if (start == end)
            return nums[start];

        int middle = (end + start) / 2;
        int max = nums[middle];
        int current = nums[middle];
        for (int i = middle-1; i >= start; i--) {
            current += nums[i];
            if (current > max) {
                max = current;
            }
        }

        current = max;

        for (int i = middle+1; i <= end; i++) {
            current += nums[i];
            if (current > max) {
                max = current;
            }
        }

        int left = helper(start, middle-1);
        int right = helper(middle+1, end);

        return Math.max(Math.max(left, right), max);
    }
}
```
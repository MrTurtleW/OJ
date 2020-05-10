需要保存两个状态：最小值和最大值

# 分治

```java
class Solution {
    private int[] nums;
    public int maxProduct(int[] nums) {
        this.nums = nums;
        return helper(0, nums.length-1);
    }

    private int helper(int start, int end) {
        if (start > end)
            return Integer.MIN_VALUE;
        if (start == end)
            return nums[start];

        int middle = (start + end ) / 2;
        int leftMax = nums[middle], leftMin = nums[middle];
        int current = nums[middle];

        for (int i=middle-1; i>=start; i--) {
            current *= nums[i];
            if (leftMax < current)
                leftMax = current;
            if (leftMin > current)
                leftMin = current;
        }

        current = 1;

        int rightMax = 1, rightMin = 1;
        for(int i=middle+1; i<= end; i++) {
            current *= nums[i];
            if (current > rightMax)
                rightMax = current;
            if (current < rightMin)
                rightMin = current;
        }

        current = Math.max(leftMax * rightMax, leftMin * rightMin);
        int left = helper(start, middle-1);
        int right = helper(middle+1, end);
        return Math.max(Math.max(left, right), current);
    }

    public static void main(String[] args) {
        int[] nums = {-2,0,-1};
        Solution solution = new Solution();
        System.out.println(solution.maxProduct(nums));
    }
}
```

# 动态规划

需要保存两个状态


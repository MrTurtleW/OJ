超时：

```java
class Solution {
    private int min_step = Integer.MAX_VALUE;
    private int[] nums;
    public int jump(int[] nums) {
        this.nums = nums;
        helper(0, 0);
        return min_step;
    }

    private void helper(int index, int step) {
        if (index == nums.length-1 && step < min_step) {
            min_step = step;
            return;
        }

        if (step >= min_step)
            return;

        if (index >= nums.length)
            return;

        for (int i = 1; i <= nums[index]; i++) {
            helper(index + i, step+1);
        }
    }
}
```


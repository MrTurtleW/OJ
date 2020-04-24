递归（超时）

```java
class Solution {
    private int[] nums;
    public int rob(int[] nums) {
        this.nums = nums;
        return helper(0);
    }

    private int helper(int index) {
        if (index >= nums.length)
            return 0;

        return Math.max(helper(index+1), helper(index+2)+nums[index]);
    }
}
```


# 动态规划

|opt|money|
|:--:|---|
|0|`$nums[0]$`|
|1|`$max(nums[0], nums[1])$`
|2|`$max(nums[0]+opt(0), opt[1])$`
|3|`$max(nums[1]+opt[1], opt[2]+nums[2])$`

```math
opt[i] = max(opt[i-2] + nums[i], opt[i-1])
```


```java
class Solution {
    public int rob(int[] nums) {
        if (nums.length == 0)
            return 0;
        if (nums.length == 1)
            return nums[0];
        int[] opt = new int[nums.length];
        opt[0] = nums[0];
        opt[1] = Math.max(nums[1], nums[0]);
        for (int i = 2; i < nums.length; i++) {
            opt[i] = Math.max(opt[i-2] + nums[i], opt[i-1]);
        }
        return opt[nums.length-1];
    }
}
```
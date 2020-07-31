```java
class Solution {
    public boolean canJump(int[] nums) {
        int length = nums.length;
        int end = 0;
        int maxPosition = 0;
        for (int i = 0; i < length; i++) {
            if (maxPosition < i)
                break;
            maxPosition = Math.max(maxPosition, i + nums[i]);
            if (i == end) {
                end = maxPosition;
            }
        }
        return maxPosition >= nums.length - 1;
    }
}
```


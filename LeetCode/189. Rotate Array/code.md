# 题解

假设`$k=2$`

1. 先把整个数组反过来，如把`[1, 2, 3, 4, 5]`变为`[5, 4, 3, 2, 1]`
2. 然后翻转前`$k$`个数，得到`[4, 5, 3, 2, 1]`
3. 翻转后面的数，得到`[4, 5, 1, 2, 3]`

```java
class Solution {
    public void rotate(int[] nums, int k) {
        if (nums.length < 2)
            return;

        k = k % nums.length;

        reverse(nums, 0, nums.length-1);
        reverse(nums, 0, k-1);
        reverse(nums, k, nums.length-1);
    }

    private void reverse(int[] nums, int start, int end) {
        for (; start < end; start++, end--) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
        }
    }
}
```
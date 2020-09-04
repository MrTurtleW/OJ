```java
class Solution {
    public void sortColors(int[] nums) {
        if (nums == null || nums.length < 2)
            return;

        int low = 0, high = nums.length - 1;
        for (int i = 0; i <= high;) {
            if (nums[i] == 0) {
                nums[i++] = nums[low];
                nums[low++] = 0;
            }
            else if (nums[i] == 2) {
                nums[i] = nums[high];
                nums[high--] = 2;
            }
            else {
                i++;
            }
        }
    }
}
```


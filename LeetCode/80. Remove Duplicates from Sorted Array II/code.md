```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null)
            return 0;

        int count=0, index=1;

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[i-1]) {
                count = 0;
                nums[index++] = nums[i];
            }

            else if (count < 1) {
                nums[index++] = nums[i];
                count++;
            }
        }

        return index;
    }
}
```


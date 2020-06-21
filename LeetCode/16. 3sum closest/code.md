```java
import java.util.Arrays;

class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int res = nums[0] + nums[1] + nums[nums.length-1];
        for (int k=0; k < nums.length-2; k++) {
            for (int i=k+1, j=nums.length-1; i < j;) {
                int temp = nums[k] + nums[i] + nums[j];

                if (temp < target)
                    i++;
                else if (temp > target)
                    j--;
                else
                    return target;

                if (Math.abs(temp-target) < Math.abs(res-target)) {
                    res = temp;
                }
            }
        }
        return res;
    }
}
```
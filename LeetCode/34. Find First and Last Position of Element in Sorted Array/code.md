```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] res = {-1, -1};
        if (nums.length < 1)
            return res;
        int index = binarySearch(nums, target);
        if (index == -1)
            return res;

        int left = index, right = index;
        while (left >= 0 && nums[index] == nums[left])
            left --;
        while (right < nums.length && nums[index] == nums[right])
            right++;
        res[0] = left+1;
        res[1] = right-1;
        return res;
    }

    private int binarySearch(int[] nums, int target) {
        int lo = 0, hi = nums.length - 1;
        while (lo <= hi) {
            int mid = (lo + hi) / 2;
            if (nums[mid] == target)
                return mid;
            else if (nums[mid] > target)
                hi = mid - 1;
            else
                lo = mid + 1;
        }
        return -1;
    }
}
```
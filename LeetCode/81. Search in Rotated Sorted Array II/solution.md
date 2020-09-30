The idea is the same as the previous one without duplicates

1. Everytime check if `target == nums[mid]`, if so, we find it.

2. Otherwise, we check if the first half is in order (i.e., `nums[left] <= nums[mid]`). If so, go to step 3, otherwise, the second half is in order, go to step 4.

3. Check if target in the range of `[left, mid-1]` (i.e., `nums[left] <= target < nums[mid]`), if so, do search in the first half (`right=mid-1`), otherwise, search in the second half (`left=mid+1`)
4. Check if target in the range of `[mid+1, right]` (i.e., `nums[mid] < taget <= nums[right]`), if so, do search in the second half (`left=mid+1`); otherwise search in the first half (`right = mid - 1`).

The only difference is that due to the existence of duplicates, we can have `nums[left] == nums[mid]` and in that case, the first half could be out of order (e.g. `[3, 1, 2, 3, 3, 3, 3]`) and we have to deal with this case separately. In that case, it is guaranteed that `nums[right]` also equals to `nums[mid]`, so what we can do is to check if `nums[mid] == nums[left] == nums[right]` before the original logic.

```java
class Solution {
    public boolean search(int[] nums, int target) {
        int left = 0, right = nums.length-1, mid;

        while (left <= right) {
            mid = (left + right) >> 1;

            if (nums[mid] == target)
                return true;
            if (nums[left] == nums[mid] && nums[mid] == nums[right]) {
                left++;
                right--;
            }
            else if (nums[left] <= nums[mid]) {
                if (nums[left] <= target && nums[mid] > target)
                    right = mid - 1;
                else
                    left = mid + 1;
            }
            else {
                if (nums[mid] < target && nums[right] >= target)
                    left = mid + 1;
                else
                    right = mid - 1;
            }
        }
        return false;
    }
}
```


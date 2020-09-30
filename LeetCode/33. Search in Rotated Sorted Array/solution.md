```java
class Solution {
    public int search(int[] nums, int target) {
        int lo = 0, hi = nums.length-1;
        
        // find the index of the smallest value using binary search.
        while (lo < hi) {
            int mid = (lo + hi) / 2;
            if (nums[mid] > nums[hi])
                lo = mid + 1;
            else
                hi = mid;
        }
        
        // lo = hi is the index of the smallest value and also the number of places rotated.
        int rot = lo;
        lo = 0; hi = nums.length-1;
        while (lo <= hi) {
            int mid = (lo + hi) / 2;
            int realmid = (mid + rot) % nums.length;
            if (nums[realmid] == target)
                return realmid;
            if (nums[realmid] < target)
                lo = mid + 1;
            else
                hi = mid - 1;
        }
        return -1;
    }
}
```

# 不用二叉搜索

```java
public class Solution {
    public int search(int[] nums, int target) {
        int start = 0, end = nums.length - 1;
        while (start < end) {
            int mid = (start + end) / 2;
            if (nums[mid] > nums[end]) {  // eg. 3,4,5,6,1,2
                // 前半部分有序
                if (target > nums[mid] || target <= nums[end]) {
                    start = mid + 1;
                } else {
                    end = mid;
                }
            } else {  // eg. 5,6,1,2,3,4
                // 后半部分有序
                if (target > nums[mid] && target <= nums[end]) {
                    start = mid + 1;
                } else {
                    end = mid;
                }
            }
        }
        if (start == end && target != nums[start]) return -1;
        return start;
    }
}
```


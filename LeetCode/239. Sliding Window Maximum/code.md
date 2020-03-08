# 自己写的

## 暴力

```java
class Solution {
    private int largest(int[] nums, int start, int end) {
        int max = Integer.MIN_VALUE;
        for (int i = start; i < end; i++) {
            if (max < nums[i])
                max = nums[i];
        }
        return max;
    }

    public int[] maxSlidingWindow(int[] nums, int k) {
        if (nums.length == 0)
            return nums;
        int result[] = new int[nums.length - k + 1];

        for (int start = 0; start <= nums.length - k; start++) {
            result[start] = largest(nums, start, start + k);
        }
        return result;
    }
}
```

# 题解

## 双端队列

```java
import java.util.ArrayDeque;

class Solution {
    ArrayDeque<Integer> deq = new ArrayDeque<Integer>();
    int [] nums;

    public void clean_deque(int i, int k) {
        // remove indexes of elements not from sliding window
        if (!deq.isEmpty() && deq.getFirst() == i - k)
            deq.removeFirst();

        // remove from deq indexes of all elements
        // which are smaller than current element nums[i]
        while (!deq.isEmpty() && nums[i] > nums[deq.getLast()])
            deq.removeLast();
    }

    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        if (n * k == 0) return new int[0];
        if (k == 1) return nums;

        // init deque and output
        this.nums = nums;
        for (int i = 0; i < k; i++) {
            clean_deque(i, k);
            deq.addLast(i);
        }
        int [] output = new int[n - k + 1];
        output[0] = nums[deq.getFirst()];

        // build output
        for (int i  = k; i < n; i++) {
            clean_deque(i, k);
            deq.addLast(i);
            output[i - k + 1] = nums[deq.getFirst()];
        }
        return output;
    }
}
```
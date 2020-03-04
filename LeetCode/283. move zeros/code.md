# 自己写的

```python
class Solution:
    def moveToEnd(self, index):
        for i in range(index, len(self.nums)-1):
            if self.nums[i+1] == 0:
                return

            self.nums[i], self.nums[i+1] = self.nums[i+1], self.nums[i]


    def moveZeroes(self, nums):
        """
        Do not return anything, modify nums in-place instead.
        """
        self.nums = nums
        index = len(nums) -1
        while index >= 0:
            if nums[index] == 0:
                self.moveToEnd(index)

            index -= 1
```

52ms：

```python
class Solution:
    def moveZeroes(self, nums):
        """
        Do not return anything, modify nums in-place instead.
        """
        self.nums = nums
        index = len(nums) -1
        while index >= 0:
            if nums[index] == 0:
                del self.nums[index]
                self.nums.append(0)

            index -= 1
```

# Insert Index

```java
public void moveZeroes(int[] nums) {
    if (nums == null || nums.length == 0) return;        

    int insertPos = 0;
    for (int num: nums) {
        if (num != 0) nums[insertPos++] = num;
    }        

    while (insertPos < nums.length) {
        nums[insertPos++] = 0;
    }
}
```

# Swap

```java
public class Solution {
    public void moveZeroes(int[] nums) {
        int j = 0;
        for(int i = 0; i < nums.length; i++) {
            if(nums[i] != 0) {
                int temp = nums[j];
                nums[j] = nums[i];
                nums[i] = temp;
                j++;
            }
        }
    }
}
```
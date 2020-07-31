典型的贪心算法

# 反向查找出发位置

我们的目标是到达数组的最后一个位置，因此我们可以考虑最后一步跳跃前所在的位置，该位置通过跳跃能够到达最后一个位置。

如果有多个位置通过跳跃都能达到最后一个位置，那么我们应该如何选择？直观上看，我们可以**贪心**地选择距离最后一个位置最远的那个位置，也就是对应下表最小的那个位置。因此，我们可以从左到右遍历数组，选择第一个满足要求的位置。

找到最后一步跳跃前所在的位置之后，我们继续贪心地寻找倒数第二步跳跃前所在位置，以此类推，直到找到数组地开始位置。

```java
class Solution {
    public int jump(int[] nums) {
        int position = nums.length - 1;
        int steps = 0;
        while (position > 0) {
            for (int i = 0; i < position; i++) {
                if (i + nums[i] >= position) {
                    position = i;
                    steps++;
                    break;
                }
            }
        }
        return steps;
    }
}
```

# 方法二：正向查找可到达的最大位置

如果我们贪心地进行正向查找，每次找到可到达地最远位置，就可以在线性时间内得到最少地跳跃次数。

例如，对于数组`[2,3,1,2,4,2,3]`，初始位置是下标0，从下标0出发，最远可到达下标2，下标0可到达的位置中，下标1地值是3，从下标1出发可以达到更远的位置，因此第一步到达下标1.

从下标1出发，最远可到达下标4。从下标4出发可以达到更远的位置，因此第二部到达下标4.

在遍历数组时，我们不访问最后一个元素，这是一位内在访问最后一个元素之前，我们的边界一定大于等于最后一个位置，否则就无法跳到最后一个位置了。如果访问最后一个元素，在边界正好为最后一个位置的情况下，我们会增加一次不必要的跳跃次数，因此我们不必访问最后一个元素。

```java
class Solution {
    public int jump(int[] nums) {
        int length = nums.length;
        int end = 0;
        int maxPosition = 0; 
        int steps = 0;
        for (int i = 0; i < length - 1; i++) {
            maxPosition = Math.max(maxPosition, i + nums[i]); 
            if (i == end) {
                end = maxPosition;
                steps++;
            }
        }
        return steps;
    }
}
```


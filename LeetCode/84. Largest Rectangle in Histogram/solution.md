## 分治法

最大面积矩形存在于以下几种情况：

- 确定了最矮柱子以后，矩形的宽尽可能往两边延伸。
- 在最矮柱子左边的最大面积矩形（子问题）。
- 在最矮柱子右边的最大面积矩形（子问题）。

```java
public class Solution {
    public int calculateArea(int[] heights, int start, int end) {
        if (start > end)
            return 0;
        int minindex = start;
        for (int i = start; i <= end; i++)
            if (heights[minindex] > heights[i])
                minindex = i;
        return Math.max(heights[minindex] * (end - start + 1), Math.max(calculateArea(heights, start, minindex - 1), calculateArea(heights, minindex + 1, end)));
    }
    public int largestRectangleArea(int[] heights) {
        return calculateArea(heights, 0, heights.length - 1);
    }
}
```

时间复杂度：$O(n\lg n)$，元素有序时达到最坏情况，复杂度为$O(n^2)$

## 线段树

https://leetcode.com/problems/largest-rectangle-in-histogram/discuss/28941/segment-tree-solution-just-another-idea-onlogn-solution

## 栈

利用栈来存储左右边界

- 起始$-1$入栈，
- 遍历数组元素，
  - 如果当前值大于等于栈顶元素，则表明栈顶元素的右边界还没到，压入栈
  - 如果当前值小于栈顶元素，则表明栈顶元素的右边界已经找到，可以计算其面积（左边界就是栈顶元素的上一个不相等元素，否则不可能入栈）
- 清空栈，计算各个元素的面积。

```java
import java.util.Stack;

class Solution 
    public int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        stack.push(-1);

        int maxarea = 0, area = 0;
        for (int i = 0; i < heights.length; i++) {
            while (stack.peek() != -1 && heights[i] < heights[stack.peek()]){
                // 计算面积
                area = heights[stack.pop()] * (i - stack.peek() - 1);
                if(maxarea < area)
                    maxarea = area;
            }
            stack.push(i);
        }
        while (stack.peek() != -1) {
            // 这里的右边界都是到最右边
            area = heights[stack.pop()] * (heights.length - stack.peek() - 1);
            if (area > maxarea)
                maxarea = area;
        }
        return maxarea;
    }
}
```


# 自己写的

## 暴力

暴力求解，时间复杂度$O(n^3)$

```java
import java.util.Arrays;

class Solution {
    public int largestRectangleArea(int[] heights) {
        if (heights.length == 0) {
            return 0;
        }
        int largestRectangle = Arrays.stream(heights).max().getAsInt();
        for (int i = 0; i < heights.length-1; i++) {
            for (int j = i+1; j < heights.length; j++) {
                int min_height = Integer.MAX_VALUE;

                for (int k = i; k <= j; k++) {
                    if (min_height > heights[k])
                        min_height = heights[k];
                }

                int area = (j - i + 1) * min_height;
                if (area > largestRectangle) {
                    largestRectangle = area;
                }
            }
        }
        return largestRectangle;
    }
}
```

超时

## 优化的暴力

优化：对每个柱子，查找左右边界，

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        if (heights.length == 0)
            return 0;

        int largestArea = heights[0];

        for (int i = 0; i < heights.length; i++) {
            // 找到左右边界，也就是比当前值要小的
            int leftBounds = i - 1, rightBounds = i + 1;
            while (leftBounds >= 0 && heights[leftBounds] >= heights[i])
                leftBounds--;

            while (rightBounds < heights.length && heights[rightBounds] >= heights[i])
                rightBounds++;

            int area = (rightBounds - leftBounds - 1) * heights[i];
            if (area > largestArea)
                largestArea = area;
        }
        return largestArea;
    }
}
```

# 自己写的

时间复杂度`$O(n^2)$`
```java
class Solution {
    public int maxArea(int[] height) {
        int max = 0;
        int area = 0;
        for (int i = 0; i < height.length-1; i++) {
            for (int j = i+1; j < height.length; j++) {
                area = Math.min(height[i], height[j]) * (j-i);
                if(max < area)
                    max = area;
            }
        }

        return max;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] array = {1,8,6,2,5,4,8,3,7};
        System.out.println(solution.maxArea(array));
    }
}
```

# 两边往中间收敛

时间复杂度`$O(n)$`

```java
class Solution {
    /**
     * 从两边网中间收敛，只看更高的
     * 谁更小，谁就往里面挪，找更高的棒子，可能出现更优解
     */
    public int maxArea(int[] height) {
        int max = 0;
        for(int i=0, j=height.length - 1; i < j; ) {
            int minHeight = height[i] < height[j] ? height[i++]: height[j--];
            max = Math.max(max, (j-i+1) * minHeight);
        }
        return max;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] array = {1,8,6,2,5,4,8,3,7};
        System.out.println(solution.maxArea(array));
    }
}
```
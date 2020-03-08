# 自己写的

```java
import java.util.Stack;

class Solution {
    private Stack<Integer> stack;
    private int[] height;

    private int calculateCount(int current){
        int count = 0;
        while (height[stack.peek()] < height[current]) {
            count += height[current] - height[stack.pop()];
        }
        stack.pop();
        return count;
    }

    public int trap(int[] height) {
        if (height.length < 2)
            return 0;

        this.height = height;
        int count = 0, current = 0;
        stack = new Stack<>();
        int start = 0, end = height.length - 1;
        while (height[start] == 0)
            start++;
        while (height[end] == 0)
            end--;

        current = start;
        stack.push(start++);

        for (; start <= end; start++) {
            if (height[start] >= height[current]) {
                // 需要计算蓄水量
                count += calculateCount(current);
                current = start;
            }
            stack.push(start);
        }

        // 从右边计算漏掉的，左边一定有更大的数，因此直接相减即可。
        current = stack.pop();
        while (!stack.isEmpty()) {
            if (height[current] > height[stack.peek()])
                count += height[current] - height[stack.pop()];
            else {
                current = stack.pop();
            }
        }
        return count;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int height[] = {0,1,0,2,1,0,1,3,2,1,2,1};
        System.out.println(solution.trap(height));
    }
}
```

# 题解

双指针：

```c++
class Solution {
public:
    int trap(int A[], int n) {
        int left=0; int right=n-1;
        int res=0;
        int maxleft=0, maxright=0;
        while(left<=right){
            if(A[left]<=A[right]){
                if(A[left]>=maxleft) maxleft=A[left];
                else res+=maxleft-A[left];
                left++;
            }
            else{
                if(A[right]>=maxright) maxright= A[right];
                else res+=maxright-A[right];
                right--;
            }
        }
        return res;
    }
};
```
# DP

The DP solution proeeds row by row, starting from the first row, Let the maximal rectangle area at row i and row j be computed by `[right(i, j) - left(i, j)] * height(i, j)`

All the 3 variables left, right, and height can be determined by the information from previous row, and also from the current row.

- $left(i, j) = max(left(i-1,j), cur\_left)$
- $right(i,j) = min(right(i-1, j), cur\_right)$
- $height(i, j)=\begin{cases}height(i-1, j)+1,&matrix[i][j]=1\\0,&matrix[i][j]=0\end{cases}$

```c++
/* we start from the first row, and move downward;
 * height[i] record the current number of countinous '1' in column i;
 * left[i] record the left most index j which satisfies that for any index k from j to  i, height[k] >= height[i];
 * right[i] record the right most index j which satifies that for any index k from i to  j, height[k] >= height[i];
 * by understanding the definition, we can easily figure out we need to update maxArea with 
 	value (height[i] * (right[i] - left[i] + 1));
 * 
 * Then the question is how to update the array of height, left, and right
 * =================================
 * for updating height, it is easy
 * for (int j = 0; j < n; j++) {
 *    if (matrix[i][j] == '1') height[j]++;
 *    else height[j] = 0;
 * }
 * =============================================================================
 * It is a little bit tricky for initializing and updating left and right array
 * for initialization: 
 * we know initially, height array contains all 0, so according to the definition of left and right array, 
 	left array should contains all 0, and right array should contain all n - 1 ( >= height)
 * for updating left and right, it is kind of tricky to understand...
 *     ==============================================================
 *     Here is the code for updating left array, we scan from left to right
 *     int lB = 0;  //lB is indicating the left boundry for the current row of the matrix (for cells with char "1"), 
 	not the height array...
 *     for (int j = 0; j < n; j++) {
 *          if (matrix[i][j] == '1') {
 				// this means the current boundry should satisfy two conditions: 
 				// within the boundry of the previous height array, and within the boundry of the current row...
 *              left[j] = Math.max(left[j], lB); 
 *          } else {
 				// when matrix[i][j] = 0, height[j] will get update to 0, so left[j] becomes 0, 
 				// since all height in between 0 - j satisfies the condition of height[k] >= height[j];
 *              left[j] = 0; 
 *              lB = j + 1; //and since current position is '0', so the left most boundry for next "1" cell is at least j + 1;
 *          }
 *     }
 *     ==============================================================
 *     the idea for updating the right boundary is similar, we just need to iterate from right to left
 *     int rB = n - 1;
 *     for (int j = n - 1; j >= 0; j--) {
 *         if (matrix[i][j] == '1') {
 *              right[j] = Math.min(right[j], rB);
 *         } else {
 *              right[j] = n - 1;
 *              rB = j - 1;
 *      }
 */
class Solution {
    public int maximalRectangle(char[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0] == null || matrix[0].length == 0)
            return 0;

        int m = matrix.length, n = matrix[0].length, maxArea = 0;

        int[] left = new int[n];
        int[] right = new int[n];
        int[] height = new int[n];

        Arrays.fill(right, n-1);

        for (char[] chars : matrix) {
            int rB = n - 1;
            for (int j = n - 1; j >= 0; j--) {
                if (chars[j] == '1')
                    right[j] = Math.min(right[j], rB);
                else {
                    right[j] = n - 1;
                    rB = j - 1;
                }
            }

            int lB = 0;
            for (int j = 0; j < n; j++) {
                if (chars[j] == '1') {
                    left[j] = Math.max(left[j], lB);
                    height[j]++;
                    maxArea = Math.max(maxArea, height[j] * (right[j] - left[j] + 1));
                } else {
                    height[j] = 0;
                    left[j] = 0;
                    lB = j + 1;
                }
            }
        }
        return maxArea;
    }
}
```

# Histogram

参考 [84题](https://leetcode.com/problems/largest-rectangle-in-histogram/discuss/28900/short-and-clean-on-stack-based-java-solution)

这个matrix有m行，就把这个问题转换成m个Histogram的问题，每个问题就是一个以这一行为底的Histogram问题，上面连续的1的个数就是Height。

```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        if(matrix.length == 0) return 0;
        int n = matrix[0].length;
        int[] heights = new int[n]; // using a array to reduce counting step of 1
        int max = 0;
        for(char[] row: matrix){
            for(int i = 0; i < n; i++){
                if(row[i] == '1'){
                    heights[i] += 1;
                } else {
                    heights[i] = 0;
                }
            }

            max = Math.max(max, maxArea(heights)); // go a sub problem of Histogram
        }
        return max;
    }

    // Exact same solution to Histogram
    public int maxArea(int[] heights){
        Stack<Integer> stack = new Stack();
        int max = 0;
        for(int i = 0; i <= heights.length; i++){
            int h = (i == heights.length) ? 0 : heights[i];
            while(!stack.isEmpty() && heights[stack.peek()] > h){
                int index = stack.pop();
                int leftBound = -1;
                if(!stack.isEmpty()){
                    leftBound =  stack.peek();
                }
                max = Math.max(max, heights[index] * (i - leftBound - 1));
            }
            stack.push(i);
        }
        return max;
    }
}
```


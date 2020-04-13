```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    private List<List<Integer>> triangle;
    public int minimumTotal(List<List<Integer>> triangle) {
           this.triangle = triangle;
           return helper(0, 0);
    }

    private int helper(int row, int col) {
        if (row < triangle.size() && col < triangle.get(row).size()) {
            int currentVal = triangle.get(row).get(col);
            return currentVal + Math.min(helper(row+1, col), helper(row+1, col+1));
        }

        return 0;
    }

    public static void main(String[] args) {
        List<List<Integer>> triangle = new ArrayList<>();
        triangle.add(Arrays.asList(2));
        triangle.add(Arrays.asList(3, 4));
        triangle.add(Arrays.asList(6, 5, 7));
        triangle.add(Arrays.asList(4, 1, 8, 3));

        Solution solution = new Solution();
        System.out.println(solution.minimumTotal(triangle));
    }
}
```

超时

加缓存：

```java
class Solution {
    private List<List<Integer>> triangle;
    private List<List<Integer>> opt;
    public int minimumTotal(List<List<Integer>> triangle) {
           this.triangle = triangle;

           opt = new ArrayList<>();
           for (int i = 0; i < triangle.size(); i++) {
               List<Integer> local = new ArrayList<>();
               for (int j = 0; j < triangle.get(i).size(); j++) {
                   local.add(0);
               }
               opt.add(local);
           }

           return helper(0, 0);
    }

    private int helper(int row, int col) {
        if (row >= triangle.size() || col >= triangle.get(row).size())
            return 0;

        if (opt.get(row).get(col) != 0)
            return opt.get(row).get(col);
        
        int val = triangle.get(row).get(col);
        if (row != triangle.size() - 1) {
            val += Math.min(helper(row+1, col), helper(row+1, col+1));
        }
        opt.get(row).set(col, val);
        return val;
    }
}
```

动态规划：

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        List<List<Integer>> opt = new ArrayList<>();
         for (int i = 0; i < triangle.size(); i++) {
             List<Integer> local = new ArrayList<>();
             for (int j = 0; j < triangle.get(i).size(); j++) {
                 local.add(0);
             }
             opt.add(local);
         }

         // 最后一行填充好数据
         for(int i =0; i < triangle.get(triangle.size()-1).size(); i++) {
             opt.get(triangle.size()-1).set(i, triangle.get(triangle.size()-1).get(i));
         }

        // 从下往上填充，因为下面的已知，所以直接取较小的，加上当前值即可
         for (int i = triangle.size()-2; i >= 0; i--) {
             for (int j = triangle.get(i).size()-1; j >=0; j--) {
                 int smaller = Math.min(opt.get(i+1).get(j), opt.get(i+1).get(j+1));
                 opt.get(i).set(j, triangle.get(i).get(j) + smaller);
             }
         }
         return opt.get(0).get(0);
    }
}
```
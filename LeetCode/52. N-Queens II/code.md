```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    private int n;
    private int res;

    public int totalNQueens(int n) {
        this.n = n;
        dfs(new ArrayList<Integer>(), new ArrayList<Integer>(), new ArrayList<Integer>());
        return res;
    }

    /**
     * 遍历查找符合条件的
     * @param queens 如果第i个元素的值为j，那么表示当前棋盘上i行j列放有皇后
     * @param xySum  行和列的加和，用于判断是否同行同列
     * @param xySub  行和列相减，用于判断是否在对角线上
     */
    private void dfs(List<Integer> queens, List<Integer> xySum, List<Integer> xySub) {
        if (queens.size() == n) {
            res++;
        }

        for(int i=0; i< n; i++) {
            if (queens.contains(i) || xySub.contains(queens.size() - i) || xySum.contains(queens.size() + i)){
            }
            else {
                xySub.add(queens.size() - i);
                xySum.add(queens.size() + i);
                queens.add(i);
                dfs(queens, xySum, xySub);
                queens.remove(queens.size()-1);
                xySub.remove(xySub.size()-1);
                xySum.remove(xySum.size()-1);
            }
        }
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.totalNQueens(4));
    }
}
```


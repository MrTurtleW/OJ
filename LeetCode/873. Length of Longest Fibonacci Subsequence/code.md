暴力dfs：

```java
class Solution {
    private int[] A;
    private int res = 0;
    public int lenLongestFibSubseq(int[] A) {
        this.A = A;
        helper(new ArrayList<>(), 0);
        return res;
    }

    private void helper(List<Integer> tempRes, int start) {
        int size = tempRes.size();
        if (size > 2 && tempRes.get(size-3) + tempRes.get(size-2) != tempRes.get(size-1))
            return;

        if (size > 2 && start == A.length && tempRes.size() > res) {
            res = tempRes.size();
            return;
        }

        for (int i=start; i<A.length; i++) {
            helper(new ArrayList<>(tempRes), i+1);
            tempRes.add(A[i]);
            helper(new ArrayList<>(tempRes), i+1);
            tempRes.remove(tempRes.size()-1);
        }
    }
}
```

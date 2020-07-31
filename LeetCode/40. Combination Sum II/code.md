```java
class Solution {
    private List<List<Integer>> res = new LinkedList<>();
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        helper(candidates, new LinkedList<>(), 0, target);
        return res;
    }

    private void helper(int[] candidates, List<Integer> temp, int index, int target) {
        if (target == 0) {
            res.add(new LinkedList<>(temp));
            return;
        }
        if (index >= candidates.length)
            return;
        if (target < 0)
            return;

        int current = candidates[index];
        temp.add(current);
        helper(candidates, temp, index+1, target-current);
        temp.remove(temp.size()-1);

        while (index < candidates.length && candidates[index] == current) {
            index++;
        }
        helper(candidates, temp, index, target);
    }
}
```
```java
class Solution {
    private List<List<Integer>> res = new ArrayList<>();
    private int[] nums;
    public List<List<Integer>> subsets(int[] nums) {
        this.nums = nums;
        helper(new ArrayList<Integer>(), 0);
        return res;
    }

    private void helper(List<Integer> list, int i) {
        if (i == nums.length) {
            res.add(new ArrayList<>(list));
            return;
        }
        helper(list, i+1);
        list.add(nums[i]);
        helper(list, i+1);
        list.remove(list.size()-1);
    }
}
```

按照题解自己写的：

```java
class Solution {
    private List<List<Integer>> res = new ArrayList<>();
    private int[] nums;
    public List<List<Integer>> subsets(int[] nums) {
        this.nums = nums;
        helper(new ArrayList<>(), 0);
        return res;
    }

    private void helper(List<Integer> list, int i) {
        res.add(new ArrayList<>(list));
        for (; i< nums.length; i++) {
            list.add(nums[i]);
            helper(list, i+1);
            list.remove(list.size()-1);
        }
    }
}
```
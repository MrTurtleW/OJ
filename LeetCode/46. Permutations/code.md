# 自己写的

```java
class Solution {
    private List<List<Integer>> result = new LinkedList<>();
    public List<List<Integer>> permute(int[] nums) {
        List<Integer> numsList = Arrays.stream(nums).boxed().collect(Collectors.toList());
        helper(numsList, new LinkedList<>());
        return result;
    }

    private void helper(List<Integer> numsList, List<Integer> temp) {
        if (numsList.size() == 0) {
            result.add(new ArrayList<>(temp));
            return;
        }

        for (int i = 0; i < numsList.size(); i++) {
            Integer num = numsList.get(i);
            numsList.remove(num);
            temp.add(num);
            helper(numsList, temp);
            temp.remove(num);
            numsList.add(i, num);
        }
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3};
        Solution solution = new Solution();
        solution.permute(nums);
    }
}
```

# 题解

```java
public List<List<Integer>> permute(int[] nums) {
   List<List<Integer>> list = new ArrayList<>();
   // Arrays.sort(nums); // not necessary
   backtrack(list, new ArrayList<>(), nums);
   return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int [] nums){
   if(tempList.size() == nums.length){
      list.add(new ArrayList<>(tempList));
   } else{
      for(int i = 0; i < nums.length; i++){ 
         if(tempList.contains(nums[i])) continue; // element already exists, skip
         tempList.add(nums[i]);
         backtrack(list, tempList, nums);
         tempList.remove(tempList.size() - 1);
      }
   }
} 
```
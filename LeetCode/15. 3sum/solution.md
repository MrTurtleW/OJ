# 暴力求解

```java
import java.util.*;
import java.util.stream.Collectors;

class Solution {

    private List<List<Integer>> result = new ArrayList<>();

    private boolean checkListDuplicate(List<Integer> l1, List<Integer> l2){
        for (Integer i: l1){
            if(!l2.contains(i)){
                return false;
            }
        }
        return true;
    }

    private boolean checkDuplicate(List<Integer> list){
        for (List<Integer> next : result) {
            if (checkListDuplicate(next, list))
                return true;
        }
        return false;
    }
    public List<List<Integer>> threeSum(int[] nums) {

        for (int i = 0; i < nums.length-2; i++) {
            for (int j = i+1; j < nums.length-1; j++) {
                for (int k = i+2; k < nums.length; k++) {
                    if(nums[i]+nums[j]+nums[k] == 0){
                        List<Integer> list = new ArrayList<>();
                        list.add(nums[i]);
                        list.add(nums[j]);
                        list.add(nums[k]);
                        if(!checkDuplicate(list))
                            result.add(list);
                    }
                }
            }
        }
        return result;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] nums = {-1, 0, 1, 2, -1, -4};
        System.out.println(solution.threeSum(nums));
    }
}
```

# 哈希表



# 双指针
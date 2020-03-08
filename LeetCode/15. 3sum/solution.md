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

```java
import java.util.*;

class Solution {

    private List<List<Integer>> result = new ArrayList<>();

    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        // 固定k
        for(int k=0; k<nums.length-2; k++){
            // 因为已排好序，当前值大于0，那么以后的值都大于0
            if(nums[k] > 0)
                break;

            // 重复值，跳过
            if(k > 0 && nums[k] == nums[k-1])
                continue;

            // 查找
            for (int i = k+1, j=nums.length-1; i < j;) {
                int s = nums[i] + nums[j] + nums[k];
                // j太大
                if (s > 0) {
                    while(nums[j--] == nums[j] && j > 0);
                }
                // i太小
                else if (s < 0) {
                    while(nums[i++] == nums[i] && i < j);
                }
                else{
                    result.add(new ArrayList<>(Arrays.asList(nums[k], nums[i], nums[j])));
                    while(nums[j--] == nums[j] && j > 0);
                    while(nums[i++] == nums[i] && i < j);
                }

            }
        }
        return result;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] array = {-4,-2,1,-5,-4,-4,4,-2,0,4,0,-2,3,1,-5,0};
        System.out.println(solution.threeSum(array));
    }
}
```
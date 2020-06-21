```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> list = new LinkedList<>();
        Arrays.sort(nums);
        for (int i=0; i<nums.length-3;) {
            for (int j=i+1; j<nums.length-2;) {
                for (int k=j+1, l=nums.length-1; k < l;) {
                    int temp = nums[i] + nums[j] + nums[k] + nums[l];

                    if (temp < target) {
                        while (k< nums.length-1 && nums[k++]==nums[k]);
                    }
                    else if (temp > target) {
                        while (l > 0 &&nums[l--] == nums[l]);
                    }
                    else {
                        List<Integer> tempList = new LinkedList<>();
                        tempList.add(nums[i]);
                        tempList.add(nums[j]);
                        tempList.add(nums[k]);
                        tempList.add(nums[l]);
                        list.add(tempList);

                        while (k< nums.length-1 && nums[k++]==nums[k]);
                        while (l > 0 &&nums[l--] == nums[l]);
                    }
                }
                while (j< nums.length-2 && nums[j++]==nums[j]);
            }
            while (i< nums.length-3 && nums[i++]==nums[i]);
        }
        return list;
    }
}
```
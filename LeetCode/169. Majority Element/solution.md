Boyer-Moore Majority Vote Algorithm

```java
public class Solution {
    public int majorityElement(int[] num) {

        int major=num[0], count = 1;
        for(int i=1; i<num.length;i++){
            // 如果前面已经查找了 i 个元素，但cnt == 0 ，
            // 这说明前面i 个元素都没有 majority，或者有 majority，
            // 但是出现的次数少于 i / 2 ；
            // 因为如果多于 i / 2 的话 cnt 就一定不会为 0 。
            // 此时剩下的 n - i 个元素中，majority 的数目依然多于 (n - i) / 2，
            // 因此继续查找就能找出 majority
            if(count==0){
                count++;
                major=num[i];
            }else if(major==num[i]){
                count++;
            }else count--;
            
        }
        return major;
    }
}
```

排序：

```java
public class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
	    int len = nums.length;
	    return nums[len/2];
    }
}
```
在不重复的情况下生成幂集：

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        for (int num : nums) {
            int size = res.size();
            for (int i = 0; i < size; i++) {
                List<Integer> temp = new ArrayList<>(res.get(i));
                temp.add(num);
                res.add(temp);
            }
            List<Integer> temp = new ArrayList<>();
            temp.add(num);
            res.add(temp);
        }
		res.add(new ArrayList<>());
        return res;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        List<List<Integer>> result = solution.subsetsWithDup(new int[]{1,2,3});
        for (List<Integer> r : result) {
            System.out.println(r);
        }
    }
}
```

如果可能重复，先排序，并且记录上一次队列有多少元素，碰到重复的元素时只需要在最后一次入队列的元素上添加即可。

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        int lastIndex = 0;
        for (int index = 0; index < nums.length; index++) {
            int size = res.size();
            int i = 0;

            // 碰到重复的元素，需要在最后一次入队的基础上添加新元素
            if (index > 0 && nums[index] == nums[index-1]) {
                i = lastIndex;
            }
            else {
                List<Integer> temp = new ArrayList<>();
                temp.add(nums[index]);
                res.add(temp);
            }

            lastIndex = size;
            for (; i < size; i++) {
                List<Integer> temp = new ArrayList<>(res.get(i));
                temp.add(nums[index]);
                res.add(temp);
            }

        }
        res.add(new ArrayList<>());
        return res;
    }
}
```


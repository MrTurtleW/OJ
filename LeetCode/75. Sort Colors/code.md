```java
class Solution {
    public void sortColors(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();

        for (int num: nums) {
            if (map.containsKey(num))
                map.put(num, map.get(num) + 1);
            else
                map.put(num, 1);
        }

        int index = 0;
        for (int i : new int[]{0, 1, 2}) {
            if (!map.containsKey(i))
                continue;
            for (int j = 0; j < map.get(i); j++) {
                nums[index++] = i;
            }
        }
    }
}
```

